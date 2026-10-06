# Day 0: Setup checklist (do this before Week 1, ~60–90 min)

Everything here is **free** or **already included in your Claude Pro/Max subscription**. Nothing else needs to be bought.

[Plan overview](README.md)

## 1. Accounts and plan
- [ ] **Claude account on Pro or Max.** Claude Code, Research, Claude Design, Cowork, Claude in Chrome and the Office add-ins need a paid plan. Check yours in **Settings → Billing**.
- [ ] **GitHub account.** You have one; Paramur and Auralis live there.
- [ ] Optional: sign in to **Claude Academy** at [academy.claude.com](https://academy.claude.com) with your Claude account, for the free courses and badges.

> **How usage works:** your plan has a **5-hour session limit plus a weekly limit**, shared across claude.ai, Desktop, mobile and Claude Code. Bigger models, higher effort and parallel agents use more. Check **Settings → Usage** (or `/usage` in Claude Code). ⚠️ Avoid things billed as extra **usage credits** unless you decide otherwise: Fable models on Pro, fast mode, and ultrareview after the free runs.

## 2. Apps (all free downloads)
- [ ] **Claude Desktop** (macOS, Windows; Linux in beta): [claude.ai/download](https://claude.ai/download). Includes Chat, Cowork and the **Code** tab.
- [ ] **Claude mobile app** (iOS, Android). Turn on voice mode and add the widget.
- [ ] **Claude in Chrome** extension, from the Chrome Web Store. Use a **separate Chrome profile** without banking or health accounts (Week 3).
- [ ] Optional: **Claude for Microsoft 365** (Excel, PowerPoint, Word) from Microsoft AppSource, and **Claude for Google Workspace** (beta) if you use Google Docs or Sheets.

## 3. Claude Code (included in Pro/Max)
- [ ] **Install the CLI:**
  - macOS/Linux/WSL: `curl -fsSL https://claude.ai/install.sh | bash`
  - Windows (PowerShell): `irm https://claude.ai/install.ps1 | iex`
- [ ] Run `claude`, then `/login` with your claude.ai account, then `/status` to confirm.
- [ ] Open **claude.ai/code** (you already use it) and check that the Claude GitHub App has access to Paramur and Auralis.
- [ ] Optional: the **VS Code** extension ("Claude Code"), free in the VS Code Marketplace.

## 4. Free developer tools (for Weeks 3–6)
- [ ] **Git**, from [git-scm.com](https://git-scm.com).
- [ ] **Node.js LTS**, from [nodejs.org](https://nodejs.org). Needed for `npx`-based MCP servers such as Playwright and MCP Inspector.
- [ ] **Python 3.11+** and **uv**, from [docs.astral.sh/uv](https://docs.astral.sh/uv). Paramur is Python, and uv runs Python MCP servers.
- [ ] **jq**, for hook scripts (`brew install jq` / `winget install jqlang.jq`).
- [ ] **VS Code** (free) as your editor.

## 5. Settings to check once (claude.ai → Settings)
- [ ] **Profile / personal preferences:** who you are, your languages (DE/EN/ES), how you like answers.
- [ ] **Capabilities:** turn on *Code execution and file creation* (needed for files, artifacts and skills), web search and memory as you prefer.
- [ ] **Privacy:** at claude.ai/settings/data-privacy-controls, decide whether chats may be used for model training. Allowing it means up to 5 years of retention; otherwise it's 30 days.
- [ ] **Connectors:** Gmail, Google Calendar and Google Drive are already connected. Review their permissions.

## 6. Your learning workspace
- [ ] Keep this plan open: the [README](README.md) has a **progress tracker**.
- [ ] Create a **private** note or doc called **"AI Playbook"** (template in the README). ⚠️ This Learning repository is **public**, so don't store client data, prices, credentials or internal details here.
- [ ] Block the time: **45–60 min on weekdays, 90 min on Saturdays, 30 min on Sundays**. Tip: ask Claude (Calendar connector) to propose and create the blocks for you.

✅ **Setup done.** Start with [Week 1](week-1-ai-foundations-and-prompting.md).
