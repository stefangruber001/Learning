# Claude Code cheat sheet

Checked against the official docs (code.claude.com/docs) in October 2026. Claude Code updates almost daily, so check `/release-notes` or the weekly [What's new](https://code.claude.com/docs/en/whats-new/index) digest.

## Install and start
| Task | Command |
|---|---|
| Install (macOS/Linux/WSL) | `curl -fsSL https://claude.ai/install.sh \| bash` |
| Install (Windows PowerShell) | `irm https://claude.ai/install.ps1 \| iex` |
| Start / sign in | `claude` → `/login` |
| Continue last session / pick one | `claude --continue` / `claude --resume` |
| Start a cloud session from the terminal | `claude --cloud "task"` |
| Pull a cloud session into the terminal | `claude --teleport` |
| One-shot (headless) | `claude -p "prompt"` (add `--output-format json`) |
| Background sessions dashboard | `claude agents` |
| Isolated parallel session | `claude --worktree` |

## Keys you'll use daily
| Key | What it does |
|---|---|
| `Shift+Tab` | Cycle permission modes: Manual → acceptEdits → plan → (bypass) → auto |
| `Esc` | Interrupt Claude (it keeps the work done so far) |
| `Esc` `Esc` | Clear the draft, or on an empty prompt open the **rewind** menu |
| `!cmd` | Run a shell command; Claude sees the output |
| `@path` | Mention a file (autocomplete) |
| `Ctrl+V` | Paste an image or screenshot |
| `Ctrl+R` | Search prompt history |
| `Ctrl+B` | Send the running command or agent to the background |
| `Ctrl+O` | Transcript viewer (see every tool call) |
| `Ctrl+T` | Show or hide Claude's task checklist |
| `Ctrl+G` | Edit your prompt in your text editor |
| `Ctrl+S` | Stash the prompt and restore it later |
| `Option/Alt+P` | Switch model without losing your prompt |
| Type while Claude works | Your message is **queued** and sent next |

## Commands by job
**Context and memory:** `/init` · `/memory` · `/context` · `/compact [focus]` · `/clear` · `/btw <question>` · `/doctor prompt-audit` · `/rewind` · `/branch` · `/recap`

**Planning and doing:** `/plan [task]` · `/goal <condition>` · `/loop [interval] <prompt>` · `/batch <instruction>` · `/run` · `/verify` · `/subtask` · `/fork` · `/background` · `/tasks`

**Review and quality:** `/diff` · `/code-review [effort] [--fix] [--comment]` · `/security-review` · `/simplify` · `/autofix-pr` · `/ultrareview` (⚠️ 3 free runs, then paid)

**Configure:** `/config` · `/permissions` · `/fewer-permission-prompts` · `/sandbox` · `/model` · `/effort` · `/output-style` · `/statusline` · `/theme` · `/keybindings` · `/hooks` · `/mcp` · `/plugin` · `/skills` · `/skill-doctor` · `/update-config`

**Surfaces and integrations:** `/desktop` · `/mobile` · `/remote-control` · `/teleport` · `/remote-env` · `/web-setup` · `/install-github-app` · `/install-slack-app` · `/chrome` · `/voice` · `/schedule` (routines)

**Design and visual:** `/design [brief]` · `/design-sync` · `/design-login` · `/slides [brief]` · `/dataviz` · `/artifacts`

**Learn and inspect:** `/powerup` (interactive lessons) · `/insights` (usage report, local only) · `/usage` · `/status` · `/release-notes` · `/help` · `/team-onboarding`

> In **cloud sessions** (claude.ai/code), text commands work, but terminal-UI commands such as `/plugin`, `/resume`, `/insights` and `/powerup` need the local CLI or Desktop.

## Permission modes
| Mode | Claude may… | Use for |
|---|---|---|
| **Manual** (default label) | ask before edits and commands | Learning, sensitive repos |
| **acceptEdits** | edit files without asking | Trusted iteration |
| **plan** | read and research only, then propose | Anything multi-file. Start here |
| **auto** | act; a classifier blocks risky actions | Everyday work (default in recent versions) |
| **dontAsk** | only pre-approved tools | CI scripts |
| **bypassPermissions** | everything | Throwaway sandboxes only ⚠️ |

## Files that shape Claude Code
| File | Purpose |
|---|---|
| `~/.claude/CLAUDE.md` | Your personal instructions (all projects) |
| `CLAUDE.md` or `.claude/CLAUDE.md` | Project instructions (commit). Keep under ~200 lines |
| `CLAUDE.local.md` | Personal project notes (gitignore) |
| `.claude/rules/*.md` with `paths:` | Rules that load only for matching files |
| `.claude/settings.json` / `settings.local.json` / `~/.claude/settings.json` | Permissions, hooks, env, model… |
| `.claude/skills/<name>/SKILL.md` | Project skills (`/name`). Work in cloud sessions |
| `~/.claude/skills/<name>/SKILL.md` | Personal skills (local only) |
| `.claude/agents/<name>.md` | Custom subagents |
| `.mcp.json` | Project MCP servers (work in cloud sessions) |
| `.claude-plugin/plugin.json` / `marketplace.json` | Plugin and marketplace manifests |

## Minimal templates
**Skill:** `.claude/skills/weekly-summary/SKILL.md`
```markdown
---
name: weekly-summary
description: Use when the user asks for a weekly summary of repository changes.
disable-model-invocation: true
---
Recent commits:
!`git log --since="7 days ago" --oneline`

Write a 5-bullet summary for non-technical readers in German and English.
```

**Subagent:** `.claude/agents/reviewer.md`
```markdown
---
name: reviewer
description: Read-only reviewer. Use after any non-trivial change to find bugs and risky assumptions.
tools: Read, Grep, Glob
model: sonnet
---
You are a skeptical senior reviewer. Report concrete problems with file:line and a suggested fix. No praise, no style nits.
```

**Hook:** block edits to secret files (`.claude/settings.json`)
```json
{
  "hooks": {
    "PreToolUse": [
      { "matcher": "Edit|Write",
        "hooks": [ { "type": "command", "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/hooks/protect-files.sh" } ] }
    ]
  }
}
```
```bash
#!/bin/bash
# .claude/hooks/protect-files.sh  (chmod +x)
FILE_PATH=$(jq -r '.tool_input.file_path // empty')
for p in ".env" ".git/" "secrets"; do
  if [[ "$FILE_PATH" == *"$p"* ]]; then
    echo "Blocked: $FILE_PATH is protected. Ask the owner to edit it." >&2
    exit 2
  fi
done
exit 0
```

**MCP:**
```bash
claude mcp add --transport http claude-code-docs https://code.claude.com/docs/mcp     # free docs server
claude mcp add --scope project playwright -- npx -y @playwright/mcp@latest            # browser automation
claude mcp list        # check status
```

## Free vs. costs extra (on Pro/Max)
- ✅ **Included:** CLI, Desktop, web and mobile sessions, skills, subagents, hooks, MCP, plugins, routines, GitHub Actions with `claude setup-token`, artifacts, `/design`. All of it counts against your plan's usage limits.
- ⚠️ **Extra cost (usage credits):** fast mode (`/fast`), `/ultrareview` after 3 free runs, API-key usage (`--bare`, Agent SDK with an API key).
- 💡 **Save limits:** use `sonnet` or `haiku` and lower `/effort` for simple tasks, start a fresh session per task, keep CLAUDE.md lean, and disable unused plugins and MCP servers.
