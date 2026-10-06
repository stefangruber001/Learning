# Week 5: Claude Code advanced: skills, subagents, hooks, plugins and automation

> **Theme:** Stop repeating yourself. Turn your best workflows into reusable skills, specialist subagents, guaranteed hooks and scheduled automations, then package them so every project benefits.
> **Main surfaces:** Claude Code (CLI, Desktop or cloud), claude.ai/code/routines and GitHub.
> **Projects:** Paramur and Auralis. You already have custom subagents in both, so this week makes them sharper.

← [Week 4](week-4-claude-code-foundations.md) · [Plan overview](README.md) · [Week 6 →](week-6-claude-design-and-capstone.md)

---

## Day 29 · Mon: Skills, or teaching Claude your repeatable workflows

**Goal:** Build a project skill that does a real recurring job.
**Time:** ~60 min · **Where:** Claude Code · **Cost:** included

### Theory (15 min)
- **A skill is a folder with a `SKILL.md`.** It holds YAML frontmatter (at least `name` and `description`), then instructions, plus optional scripts, templates or reference files.
- **Progressive disclosure.** Only the *description* sits in context all the time. The full skill loads when it's used, which is why skills scale far better than stuffing CLAUDE.md.
- **Invocation.** Type `/skill-name [args]`, or Claude uses the skill automatically when your request matches the description, so write descriptions like *"Use when…"*.
- **Custom commands were merged into skills.** `.claude/commands/x.md` still works, but new things should be skills.
- **Locations:**
  - `~/.claude/skills/<name>/SKILL.md` is personal. ⚠️ It isn't available in cloud sessions or routines.
  - `.claude/skills/<name>/SKILL.md` is the project version. Commit it so it's shared and works in the cloud.
- **Useful frontmatter:**
  - `description`: when to use the skill.
  - `disable-model-invocation: true`: only *you* can trigger it, e.g. for deploys.
  - `allowed-tools`: tools that run without asking.
  - `argument-hint`: hint text for arguments.
  - `context: fork`: run it as a subagent.
- **Dynamic context.** `` !`git log --oneline -20` `` inside a skill injects live command output. `$ARGUMENTS` receives what you type after the command.
- **Bundled skills worth knowing:** `/run`, `/verify`, `/batch`, `/simplify`, `/loop`, `/code-review`, `/dataviz`, `/design`, `/slides`, `/update-config`, `/fewer-permission-prompts`, `/claude-api`.
- `/skills` lists your skills. **`/skill-doctor`** shows each skill's context cost and how often it's used.

### Practice (45 min)
**Paramur:** create a `release-notes` skill. Paramur already keeps "What's new" documents per version, and this automates the next one.
> Create a project skill at .claude/skills/release-notes/SKILL.md. When invoked as /release-notes [version], it should: read the existing "What's new" documents as style examples, inject `git log` since the last version, and draft the next document in German and English for partners (non-technical, benefit-first, max 10 bullets). Use disable-model-invocation: true. Show me the SKILL.md before saving.

Then start a fresh session and run `/release-notes vXX`.

**Auralis alternative:** a `/new-faq` skill that adds an FAQ entry in DE/EN/ES, updates the "Common questions" in `llms.txt`, and reminds you of the compliance wording (coaching, not medical advice).

### ✅ Done when
- The skill shows in `/skills`, works in a fresh session, and the output needs only light edits.

### 💡 Smart idea
Every time you paste the same instructions twice, turn them into a skill. Good candidates: offer emails, Instagram captions in brand voice, a translation check, and your app-store release checklist.

📖 [Skills in Claude Code](https://code.claude.com/docs/en/skills) · [Features overview: what goes where](https://code.claude.com/docs/en/features-overview)

---

## Day 30 · Tue: Subagents, or specialists with their own context

**Goal:** Understand when to delegate, then improve your existing agents and add a sharp read-only specialist.
**Time:** ~60 min · **Where:** Claude Code · **Cost:** included (parallel agents use more of your limits)

### Theory (15 min)
- **A subagent is a separate Claude instance.** It has its own context window, system prompt, tool restrictions and model, and it returns a *summary* to the main conversation.
- **Benefits:**
  - A clean main context. A huge search doesn't flood your session.
  - Parallelism.
  - Specialization.
  - Least privilege, e.g. read-only reviewers.
- **Built-ins.** **Explore** is fast read-only search. **Plan** does research in plan mode. **general-purpose** handles everything else. Claude uses them automatically.
- **Custom agents** live in `.claude/agents/<name>.md`. The frontmatter fields:
  - `name`, and a `description` that says when to delegate.
  - `tools`: restrict them!
  - `model`: `haiku`, `sonnet`, `opus`, `fable` or `inherit`.
  - `memory` (`user`/`project`/`local`) for persistent learnings.
  - `isolation: worktree` for a private repo copy.
  - `background: true`.
- **Running work in the background:**
  - `/subtask <task>` (forked subagent) or `/fork` for a background copy of the session.
  - `Ctrl+B` backgrounds the running task.
  - `/tasks` lists background work.
  - `claude agents` opens **agent view**, one screen for all background sessions.
- **Your current agents** are "big persona" builders (sg, appbuilder, google-app-builder). They're powerful, so complement them with **small, sharp, read-only** checkers.

### Practice (45 min)
1. **Audit an existing agent:**
   > Review .claude/agents/appbuilder.md against the official subagent docs. Is the description specific enough for automatic delegation? Should tools be restricted? Which model fits? Propose a diff, don't apply yet.
2. **Create a specialist (Auralis):**
   > Create .claude/agents/translation-qa.md: a read-only agent (tools: Read, Grep, Glob; model: sonnet) that checks DE/EN/ES page content for missing or inconsistent translations, tone mismatches, and any wording that sounds like a medical claim. Output a table: page, language, issue, suggested fix.
3. Use it with *"Use the translation-qa agent on the programme and FAQ sections"*, then read the report.

### ✅ Done when
- The new agent produced a useful report, and one existing agent got a better description or tool list.

### 💡 Smart idea
Pair builders with checkers: the builder agent implements, then a read-only reviewer agent (different instructions, maybe a different model) checks the result. Two perspectives catch far more than one.

📖 [Subagents](https://code.claude.com/docs/en/sub-agents) · [Run agents in parallel](https://code.claude.com/docs/en/agents) · [Agent view](https://code.claude.com/docs/en/agent-view)

---

## Day 31 · Wed: Hooks, or rules that always run

**Goal:** Turn "please always…" into guaranteed automation.
**Time:** ~60 min · **Where:** Claude Code (local CLI is best for testing) · **Cost:** included

### Theory (15 min)
- **CLAUDE.md is advice and Claude may forget it. Hooks are enforced by the harness** at lifecycle events:
  - `PreToolUse` can **block** a tool call.
  - `PostToolUse`
  - `UserPromptSubmit`
  - `Stop` fires when Claude finishes.
  - `SessionStart`
  - `Notification`
  - `PreCompact`
  - `SubagentStop`
  - …30+ events in total.
- **Format, in `settings.json`:**
  ```json
  {
    "hooks": {
      "PostToolUse": [
        { "matcher": "Edit|Write",
          "hooks": [ { "type": "command", "command": "jq -r '.tool_input.file_path' | xargs echo edited:" } ] }
      ]
    }
  }
  ```
  - The hook receives JSON on **stdin** (`tool_name`, `tool_input`, …).
  - **Exit code 2 = block.** Your stderr message goes back to Claude so it can adjust.
  - Hook types are `command`, `http`, `mcp_tool`, `prompt` and `agent`.
- `/hooks` shows what's configured. Or just say *"from now on, whenever Claude edits a Python file, run…"*, and the `update-config` skill writes the hook for you.
- ⚠️ Hooks run with *your* permissions. Read any hook before you trust it.

### Practice (45 min)
1. **Paramur: protect sensitive files.** Ask Claude to create `.claude/hooks/protect-files.sh`. It reads `.tool_input.file_path` with `jq`; if the path matches `.env`, your credentials/company-data files or `.git/`, it prints a reason to stderr and calls `exit 2`. Then register it as a `PreToolUse` hook with matcher `Edit|Write`. Test it with *"add a comment to .env"* and confirm it's blocked.
2. **Paramur: instant syntax check.** Add a `PostToolUse` hook on `Edit|Write` that runs `python -m py_compile` on edited `.py` files.
3. **Auralis: protect the mirror rule.** Add a `Stop` hook (or a small script Claude runs) that warns when the design-system stylesheet changed but the site's `index.html` didn't, or vice versa.
4. **Local machine:** add a `Notification` hook so you get a desktop alert when Claude needs you (`osascript` on macOS, a PowerShell message box on Windows; see the docs).

### ✅ Done when
- The block hook demonstrably blocks, the post-edit check fires, and both are committed in `.claude/settings.json`.

### 💡 Smart idea
Use hooks for anything with legal or financial weight (invoices, health claims, prices) and CLAUDE.md for style. Rule of thumb: **if forgetting it once would hurt, make it a hook.**

📖 [Hooks guide](https://code.claude.com/docs/en/hooks-guide) · [Hooks reference](https://code.claude.com/docs/en/hooks)

---

## Day 32 · Thu: Plugins, marketplaces, and MCP inside Claude Code

**Goal:** Install useful free plugins, connect MCP servers to Claude Code, and package your own toolkit.
**Time:** ~60 min · **Where:** local CLI (`/plugin` is terminal-only) · **Cost:** free plugins and servers

### Theory (15 min)
- **A plugin bundles** skills, subagents, hooks, MCP servers, language servers and mods into one installable unit.
- **A marketplace** is a git repo with `.claude-plugin/marketplace.json`.
  - The official `claude-plugins-official` is added automatically.
  - For the community marketplace, run `/plugin marketplace add anthropics/claude-plugins-community` and install with `@claude-community`.
- **Commands:**
  - `/plugin` browses.
  - `/plugin install <name>@claude-plugins-official` installs.
  - `/reload-plugins` reloads.
  - Disable what you don't use, because every enabled plugin costs some context.
- **Free, high-value plugins:**
  - `security-guidance`: Claude reviews its own changes for vulnerabilities.
  - **Code intelligence**, e.g. `pyright-lsp` for Python, `typescript-lsp` and `swift-lsp`. Claude sees type errors after each edit and navigates by symbol.
  - `commit-commands` and `feature-dev`.
- **MCP in Claude Code:**
  - Add a server with `claude mcp add [--scope local|project|user] <name> …`.
  - Project scope writes `.mcp.json` into the repo, which is **also how MCP works in cloud sessions**.
  - `/mcp` manages servers and `claude mcp login` handles OAuth.
  - Tool definitions load on demand (tool search), so many servers stay cheap.
- **Trust.** Plugins and MCP servers run code or reach data. Install only from sources you trust.

### Practice (45 min)
1. Run `/plugin install security-guidance@claude-plugins-official` and `/plugin install pyright-lsp@claude-plugins-official`, then make a small Python change in Paramur and watch the diagnostics.
2. **Playwright MCP for website QA (Auralis), free:**
   ```bash
   claude mcp add --scope project playwright -- npx -y @playwright/mcp@latest
   ```
   > Open https://www.auralisnatura.com at 390px width (iPhone). Screenshot the hero, the programmes and the FAQ. List layout, contrast or text-overflow issues in DE, EN and ES with a severity rating.
3. **Package your toolkit:**
   > Turn my reusable .claude setup (the sg/appbuilder/google-app-builder agents, the release-notes skill, the protect-files hook) into a plugin inside a new private repo `claude-toolkit` with a marketplace.json. Then show me how to install it in another repo.

### ✅ Done when
- Two official plugins are installed, the Playwright MCP returned real findings, and your own plugin installs from your private marketplace.

### 💡 Smart idea
Your agents are distilled from hundreds of prompts, which makes them valuable intellectual property. A private plugin marketplace makes them versioned, installable in one command, and reusable for every new product you start.

📖 [Plugins overview](https://code.claude.com/docs/en/plugins/overview) · [Anthropic's marketplaces](https://code.claude.com/docs/en/plugins/anthropic-marketplaces) · [Code intelligence plugins](https://code.claude.com/docs/en/plugins/code-intelligence) · [MCP in Claude Code](https://code.claude.com/docs/en/mcp)

---

## Day 33 · Fri: Automation: headless mode, GitHub Actions, routines and /loop

**Goal:** Let Claude work without you sitting there, safely.
**Time:** ~60 min · **Where:** CLI, claude.ai/code/routines, GitHub · **Cost:** included (counts against your plan limits)

### Theory (15 min)
- **Headless mode.** `claude -p "prompt"` prints the result and exits.
  - Pipe data in with `cat log.txt | claude -p "explain"`.
  - Add `--output-format json` for scripts, and `--allowedTools` / `--permission-mode` for control.
  - It uses your subscription login. Only `--bare` mode needs an API key.
- **GitHub Actions** (`anthropics/claude-code-action`). Mention `@claude` in an issue or PR and Claude works on it inside GitHub's runner.
  - Set it up with `/install-github-app`.
  - It can authenticate with your **subscription token** from `claude setup-token` (secret `CLAUDE_CODE_OAUTH_TOKEN`), so there are no API costs. It uses your plan limits plus GitHub's free Actions minutes.
- **Routines** (research preview) are cloud automations: a saved prompt, repos and connectors.
  - Triggers: a **schedule** (hourly at most), an **API call** or **GitHub events**.
  - Create them at claude.ai/code/routines or with `/schedule`.
  - They run unattended, so the prompt must be self-contained and say what success looks like.
- **Inside a session:**
  - `/loop 10m <prompt>` repeats a prompt while the session stays open.
  - **Desktop scheduled tasks** run locally and can use your local files and skills.
  - **Channels** push external events (CI, chat, alerts) into a running session.

### Practice (45 min)
1. **Headless (Paramur):**
   ```bash
   git log --since="7 days ago" --oneline | claude -p "Write a 5-bullet weekly changelog in German for non-technical partners. No jargon."
   ```
2. **Routine (Paramur):** at claude.ai/code/routines, or `/schedule`, create *"Every Monday 07:10: install requirements, run the test suite, check outdated Python packages, then open one GitHub issue titled 'Weekly health check <date>' with failures, risky outdated packages and suggested next steps. If everything is green, comment 'all green' on the previous issue instead."* Click **Run now** once to test.
3. **Optional, GitHub Actions:** in your local CLI inside Paramur, run `/install-github-app`, choose the subscription token, then open an issue *"@claude add a docstring to the offer number generator"* and watch it work.

### ✅ Done when
- The headless command works, the routine ran once successfully, and you know where to see and pause it.

### 💡 Smart idea
Good routine candidates for your businesses:
- **Nightly broken-link and SEO check** of your public sites.
- **Weekly dependency and security check.**
- **Monday "what changed" digest** across all your repos.
- **Auto-triage of new GitHub issues.**

Keep them few and useful. Each run uses your limits.

📖 [Headless mode](https://code.claude.com/docs/en/headless) · [GitHub Actions](https://code.claude.com/docs/en/github-actions) · [Routines](https://code.claude.com/docs/en/routines) · [Scheduled tasks and /loop](https://code.claude.com/docs/en/scheduled-tasks)

---

## Day 34 · Sat: 🛠️ Build day: parallel agents and big tasks

**Goal:** Learn when and how to scale beyond one conversation, without burning your limits.
**Time:** 90 min · **Where:** local CLI, plus Desktop or cloud · **Cost:** included, but parallel work multiplies usage, so watch `/usage`

### Theory (15 min): the parallelism menu, from small to large
| Tool | Use when |
|---|---|
| **Subagents** (Explore etc.) | One task needs a big search or side investigation |
| **`/fork`, `/subtask`, `Ctrl+B`** | Keep chatting while a copy works in the background |
| **Worktrees** (`claude --worktree`) | Several sessions edit the same repo without collisions |
| **Agent view** (`claude agents`) | You run several background sessions and want one dashboard |
| **`/batch <instruction>`** | One change applied across many files (5–30 parallel units) |
| **Dynamic workflows** (keyword `ultracode`) | Huge audits or migrations with cross-checking. ⚠️ Token-heavy |
| **Agent teams** (experimental, `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`) | Several sessions that message each other with a shared task list |
| **Projects in Claude Code** (beta, cloud) | One conversation that coordinates many cloud threads for you |

### Practice (75 min): pick one
- **Paramur docs consolidation.** Paramur has many guides as Markdown and PDF.
  > Use 3 Explore subagents in parallel to inventory every Markdown and PDF document in this repo by topic (deployment, server, compliance, marketing, apps…). Then write DOCS_INDEX.md with a one-line summary per document, and flag documents that look outdated, duplicated or contradictory.
- **Auralis translation sweep:** use `/batch` (or your translation-qa agent in parallel) to check every page section in DE/EN/ES.
- **Agent view:** in the local CLI, dispatch 2–3 background sessions (e.g. tests, docs and a small fix) with `claude agents`, and practice peeking and replying.

### ✅ Done when
- One parallel job finished and you can say which parallel tool fits which kind of task.

---

## Day 35 · Sun: 🔁 Review and reflect

**Time:** 30 min
1. Run `/skill-doctor` and turn off skills you never use. Check `/usage`.
2. Quiz:
   1. Skill vs subagent vs hook: which one for "always run the tests before finishing"?
   2. Why do personal skills in `~/.claude/skills` not appear in cloud sessions, and how do you fix that?
   3. What does exit code 2 mean in a `PreToolUse` hook?
   4. How does `.mcp.json` differ from `claude mcp add` at the default scope?
   5. How can GitHub Actions run on your subscription instead of API billing?
   6. When is a dynamic workflow worth its token cost?
3. 🎓 Free course: continue the Claude Code and agent courses in Claude Academy (see [resources](resources.md)).
4. Add your new skills, agents and hooks to your **AI Playbook**.
