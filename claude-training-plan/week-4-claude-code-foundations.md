# Week 4: Claude Code foundations

> **Theme:** Treat Claude Code as an agent that works inside your repositories. This week covers how it acts, how to give it the right context, and the core loop: explore, plan, code, verify, commit.
> **Main surfaces:** Claude Code CLI or Desktop (Code tab) for the full feature set, plus Claude Code on the web (claude.ai/code), which is what you already use.
> **Projects:** Paramur (Python/Flask business automation and tests) and Auralis (website, design system, iOS app).

← [Week 3](week-3-mcp-skills-and-agents.md) · [Plan overview](README.md) · [Week 5 →](week-5-claude-code-advanced.md)

---

## Day 22 · Mon: How Claude Code works, and your cockpit

**Goal:** Understand the agent loop, the different surfaces and the permission modes, and get a local install working.
**Time:** ~60 min · **Where:** CLI and Desktop, then a cloud session · **Cost:** included in Pro/Max

### Theory (15 min)
- **The agent loop.** Claude Code repeats one cycle: *think → act with a tool → observe the result*. Tools include reading and searching files, editing, running shell commands, web search and MCP tools. It stops when the task is done or it needs you. A chat only talks about your code; Claude Code reads it, changes it, runs your tests and commits.
- **One engine, many surfaces.**
  - **CLI** in a terminal. Has the full feature set.
  - **Desktop app, Code tab.** Parallel sessions, visual diffs, an integrated terminal and app previews.
  - **VS Code and JetBrains** extensions.
  - **Web** at claude.ai/code. Cloud sessions run in an Anthropic VM on a fresh clone of your GitHub repo.
  - **Mobile.** The Claude app's Code section.
  - **Slack.**

  Local sessions see your files. Cloud sessions keep running when your laptop is closed.
- **Permission modes.** In the CLI, `Shift+Tab` cycles through them:
  - **Manual** asks before edits and commands.
  - **acceptEdits** auto-approves file edits.
  - **plan** is read-only research followed by a proposal. Use it for anything bigger than one file.
  - **auto** lets a separate *classifier* model approve routine actions and block risky ones. It's the default in recent versions.
  - **bypassPermissions** and **dontAsk** are for sandboxes and CI only.
- **Safety nets.** Every edit is checkpointed. Press `Esc` `Esc` on an empty prompt (or run `/rewind`) to restore code and/or conversation. Git is still the real safety net, so work on branches.
- **Controls to know:**
  - `Esc` interrupts.
  - Typing while Claude works *queues* your message.
  - `!cmd` runs a shell command.
  - `@file` adds a file.
  - `Ctrl+V` pastes screenshots.
  - `/btw` asks a side question without polluting the context.
  - `Ctrl+R` searches your prompt history.

### Practice (45 min)
1. **Install the CLI.** It's included in Pro/Max.
   - macOS/Linux: `curl -fsSL https://claude.ai/install.sh | bash`
   - Windows PowerShell: `irm https://claude.ai/install.ps1 | iex`

   Then run `claude` in any folder and `/login`. Also install the **Claude Desktop app** and open its **Code** tab.
2. Run **`/powerup`** in the CLI. These are interactive lessons with animated demos. Do at least 3.
3. Open **Paramur**, either a local clone or a cloud session. Type `/plan`, then:
   > Explain this repository to me like a new senior developer joining tomorrow: main components, how a partner request flows to an offer, an order and a payment, where the tests are and how to run them, and the 5 riskiest areas to change. Don't modify anything.
4. Try the controls: `Shift+Tab` (watch the mode indicator), `!git status`, `/btw what does "idempotent" mean?`, `/context`, `/usage`. Then `Esc` `Esc` to see the rewind menu.

### ✅ Done when
- You can explain Manual, acceptEdits, plan and auto in one sentence each.
- You have a written architecture overview of Paramur. Keep it **inside the private Paramur repo** or local, never in the public Learning repo.

### 💡 Smart idea
Start every unfamiliar task with "explain before change" in plan mode. It costs a few minutes and saves hours of wrong-direction edits.

📖 [How Claude Code works](https://code.claude.com/docs/en/how-claude-code-works) · [Permission modes](https://code.claude.com/docs/en/permission-modes) · [Interactive mode shortcuts](https://code.claude.com/docs/en/interactive-mode)

---

## Day 23 · Tue: CLAUDE.md, rules and memory, or giving Claude a brain that fits

**Goal:** Learn context engineering for code, and slim down an oversized CLAUDE.md.
**Time:** ~60 min · **Where:** Claude Code (Auralis) · **Cost:** included

### Theory (15 min)
- **The context window is working memory** (200K to 1M tokens). The system prompt, CLAUDE.md files, tool definitions, every file read and every command output all fill it. Bloat makes Claude slower and costlier, and it *follows instructions less reliably*. When the window is full, Claude Code **compacts** (summarizes) it.
- **Where instructions live:**
  - `~/.claude/CLAUDE.md`: you, all projects.
  - `./CLAUDE.md` or `./.claude/CLAUDE.md`: the project, committed.
  - `./CLAUDE.local.md`: personal and gitignored.
  - CLAUDE.md files in subfolders load when Claude works there.
  - `AGENTS.md` is read too if you have no CLAUDE.md.
- **Rules of thumb from the docs:**
  - Keep each CLAUDE.md **under ~200 lines**.
  - Put area-specific rules in **`.claude/rules/*.md` with `paths:` frontmatter**, so they load only when Claude touches matching files.
  - `@path` imports organize the file but **don't save context**, because they load at launch.
  - Long reference material belongs in **skills** (loaded on demand, Week 5) or in docs that Claude reads when needed.
- **Auto memory.** Claude keeps its own notes in `MEMORY.md`, and the first 200 lines are loaded each session. View and toggle it with `/memory`.
- **Tools for this:**
  - `/init` drafts a CLAUDE.md.
  - `/context` shows a colored usage grid.
  - `/doctor prompt-audit` finds outdated or conflicting instructions.
  - `/compact [focus]` summarizes the conversation.
  - `/clear` starts fresh. In cloud sessions, start a new session instead.

### Practice (45 min) in Auralis
1. Measure first: `!wc -l -c CLAUDE.md`, then `/context`. Note how much space memory files take. Auralis's CLAUDE.md has grown very large.
2. Run `/doctor prompt-audit` and read the findings.
3. In **plan mode**:
   > Restructure our instructions. Keep a core CLAUDE.md under 200 lines: purpose, stack, how to build/test/deploy, and the non-negotiable rules (design-system ↔ site stylesheet mirror rule, health/medical-claims compliance, languages DE/EN/ES). Move area-specific rules into .claude/rules/ files with `paths:` frontmatter (e.g. ios-app/**, design-system/**, portal/**). Move history, changelogs and long explanations to docs/ (not imported). Show me the proposed file tree and what goes where before changing anything.
4. Approve, let it execute on a **branch**, and open a PR. Start a fresh session and run `/context` again. Compare.

### ✅ Done when
- The core CLAUDE.md is under 200 lines, the scoped rules exist, and `/context` shows a clearly smaller memory share.
- A test question about a scoped rule (e.g. "What's the rule for editing the design system?") still gets the right answer.

### 💡 Smart idea
**Every correction becomes a rule.** When you correct Claude twice about the same thing, add one line to the right rules file. Your instructions then improve every week instead of growing randomly.

📖 [Memory docs](https://code.claude.com/docs/en/memory) · [Context window explorer](https://code.claude.com/docs/en/context-window)

---

## Day 24 · Wed: The core loop: explore → plan → code → verify → commit

**Goal:** Use the workflow that turns Claude Code from a fast typist into a reliable engineer.
**Time:** ~60 min · **Where:** Claude Code (Paramur) · **Cost:** included

### Theory (15 min)
- **#1 best practice: give Claude a way to verify its work.** That means tests, linters, running the app, or screenshots. Without a check, "done" only means Claude thinks it's done.
- **Explore → plan → code → commit.** Let Claude read the relevant files first, then plan in plan mode, then implement, then verify, then commit. Use small steps on a branch.
- **Be specific.** Name the files, constraints, edge cases and an example. Paste the error or a screenshot. For bigger features, say *"interview me first"*.
- **Course-correct early.** Press `Esc` the moment it drifts and redirect. Rewind if needed. Keep **one task per session**.
- **Tests first (TDD with Claude):** write a failing test, confirm it fails, implement, and confirm it passes.
- **Built-in helpers:**
  - `/run` and `/verify` launch your app and observe the result.
  - `/goal <condition>` makes Claude keep working until the condition holds, e.g. "all tests pass".

### Practice (45 min) in Paramur
1. Pick one *small* item from your roadmap or to-do list (a validation, a report field, a small endpoint improvement).
2. Plan mode:
   > Read the relevant code and tests for <feature>. Propose a plan that starts with a failing test, lists the files you'll touch, and names the edge cases. Ask me anything that's unclear before coding.
3. Approve, then: `/goal the new test and all existing tests in tests/ pass`.
4. Review with `/diff`, then let Claude commit on a feature branch with a clear message and open a PR.

### ✅ Done when
- A PR exists with a new test, the green test run is shown in the session, and you understood every changed line.

### 💡 Smart idea
Ask for an **adversarial check** before you merge: *"Act as a skeptical senior reviewer. What would break in production with this change?"* It catches what the optimistic implementer missed.

📖 [Best practices for Claude Code](https://code.claude.com/docs/en/best-practices) · [Common workflows](https://code.claude.com/docs/en/common-workflows) · [/goal](https://code.claude.com/docs/en/goal)

---

## Day 25 · Thu: Git, GitHub and code review with Claude

**Goal:** Use Claude as reviewer, security auditor and PR assistant, and move work between cloud and local.
**Time:** ~50 min · **Where:** Claude Code (Paramur) · **Cost:** included (see the ultrareview note)

### Theory (15 min)
- Claude Code is fluent in git and GitHub: branches, commit messages, PRs, merge conflicts and CI logs.
- **Review toolkit:**
  - `/diff` shows working-tree changes.
  - `/code-review [low…max]` is a bug-focused review of a diff, branch or PR. Add `--fix` to apply fixes or `--comment` to post them on the PR.
  - `/security-review` looks for vulnerabilities on your branch.
  - `/simplify` runs four parallel cleanup reviewers.
  - `/autofix-pr` starts a cloud session that watches your PR and fixes CI failures and review comments.
- ⚠️ **`/ultrareview`** is a deep cloud multi-agent review. You get **3 free runs, once, ever**. After that it costs usage credits ($5–25 per review), so save it for a big, risky PR.
- **Cloud ↔ local:**
  - `claude --cloud "task"` starts a new cloud session from your terminal.
  - `claude --teleport` pulls a cloud session into your terminal.
  - `/desktop` continues a session in the Desktop app.
  - `/remote-control` lets you steer a *local* session from your phone.
- **Worktrees.** `claude --worktree` gives parallel sessions isolated copies of the repo, so they can't collide.

### Practice (35 min) in Paramur
Paramur handles partner logins, API keys and invoices, so security review matters here.
1. On yesterday's branch, run `/code-review high`, then `/security-review`.
2. For each finding, ask *"Explain this finding to me and whether it's real"*. Fix the confirmed ones.
3. Run `/autofix-pr` (or ask a cloud session to watch the PR) and see how it reacts to CI.
4. Optional: start a task at claude.ai/code, then run `claude --teleport` locally to continue it.

### ✅ Done when
- One PR has been reviewed, fixed and merged with Claude's help, and you can explain each finding in your own words.

### 💡 Smart idea
Make `/security-review` part of your personal "definition of done" for anything that touches login, payments, uploads or personal data (Auralis intake data, Paramur partner accounts).

📖 [Code review](https://code.claude.com/docs/en/code-review) · [Claude Code in the cloud](https://code.claude.com/docs/en/claude-code-on-the-web) · [Worktrees](https://code.claude.com/docs/en/worktrees)

---

## Day 26 · Fri: Make Claude Code yours: settings, permissions, styles, models and limits

**Goal:** Configure Claude Code so it's safer, quieter and cheaper on your plan limits.
**Time:** ~50 min · **Where:** CLI (some commands are terminal-only) · **Cost:** included

### Theory (15 min)
- **Settings layers**, from broadest to most specific:
  - `~/.claude/settings.json`: you.
  - `.claude/settings.json`: the project, shared.
  - `.claude/settings.local.json`: you, in this project.
  - CLI flags.

  The more specific layer wins, except managed policies. You can also set values with `/config key=value`.
- **Permissions.** Write rules like `"allow": ["Bash(pytest *)"]` and `"deny": ["Read(./.env)"]`.
  - `/permissions` edits them.
  - **`/fewer-permission-prompts`** scans your past sessions and proposes a safe allowlist.
  - `/sandbox` restricts shell commands to certain folders and hosts.
- **Models and effort.**
  - `/model` offers the aliases `opus`, `sonnet`, `haiku` and `fable`.
  - `/effort low…max` sets how hard Claude thinks.
  - Bigger isn't always better. Use Sonnet or Haiku with low effort for simple edits to save limits.
  - `/usage` shows what drives your limits.
  - ⚠️ `/fast` (fast mode) is billed as extra usage credits. Skip it.
- **Output styles.** Default, Proactive, Concise, Explanatory and **Learning**. In Learning, Claude explains its choices and leaves small pieces of code for *you* to write.
- **Comfort:**
  - `/statusline` (describe what you want to see)
  - `/theme`
  - `/keybindings`
  - Vim mode (`/config` → Editor mode)
  - `/voice` for voice dictation

### Practice (35 min)
1. In Paramur, run `/fewer-permission-prompts`, review the proposal and accept what's safe.
2. Add deny rules for anything secret, such as `.env` files and credential and config files with bank or tax data. Commit `.claude/settings.json`.
3. `/statusline show model, context window % used, current git branch`
4. `/output-style learning`, then do a tiny change in Auralis (e.g. a new FAQ line) and write the piece Claude leaves for you.
5. Run `/usage` and note which models, tools or features use most of your limits.

### ✅ Done when
- Permissions and the deny list are committed, the statusline works, and you've written at least one piece of code yourself in Learning mode.

### 💡 Smart idea
Create `~/.claude/CLAUDE.md` with your personal defaults, for example: *"Explain in English; UI texts in DE/EN/ES; always work on a branch; ask before deleting files; summarize changes in 5 bullets at the end."*

📖 [Settings](https://code.claude.com/docs/en/settings) · [Permissions](https://code.claude.com/docs/en/permissions) · [Output styles](https://code.claude.com/docs/en/output-styles) · [Model configuration](https://code.claude.com/docs/en/model-config) · [Manage costs](https://code.claude.com/docs/en/costs)

---

## Day 27 · Sat: 🛠️ Build day: ship one real improvement end-to-end

**Goal:** Combine the whole week into one shipped change.
**Time:** 90 min · **Where:** Claude Code · **Cost:** included

Pick **one**:
- **Auralis:** add or improve one FAQ or programme detail in **DE/EN/ES**, update `llms.txt` to match, respect the design-system mirror rule, and check the result at mobile width.
- **Paramur:** a small partner-portal or back-office improvement *with tests*.

**Recipe:**
1. Plan mode, with *"interview me first"*.
2. Tests or another check first.
3. Implement, then `/goal <verifiable condition>`.
4. `/code-review`, then fix.
5. Open a PR and let `/autofix-pr` keep it green.
6. Merge.

**Reflect (10 min):** What did you have to correct? Add one line per repeated correction to CLAUDE.md or a rules file.

### ✅ Done when
- The change is merged (or deployed) and at least one new rule was added from your corrections.

---

## Day 28 · Sun: 🔁 Review and reflect

**Time:** 30 min
1. In the **local CLI**, run **`/insights`**. It writes an HTML report on how you use Claude Code, where things go wrong, and features to try. Read it.
2. Quiz yourself (answers are in this week's theory):
   1. What are the 4 everyday permission modes, and when do you use plan mode?
   2. Why can a giant CLAUDE.md make Claude *worse*?
   3. What's the difference between `@imports` and `.claude/rules/` with `paths:`?
   4. What's the single most important best practice? (Hint: verification.)
   5. What does `Esc` `Esc` do on an empty prompt?
   6. Which review command has only 3 free runs?
3. 🎓 Free course: **Claude Code in action** in Claude Academy. See [resources](resources.md).
4. Update your **AI Playbook** (see the [README](README.md#your-ai-playbook)) with your 3 best prompts of the week.
