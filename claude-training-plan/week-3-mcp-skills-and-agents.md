# Week 3: MCP, skills and agentic Claude

> **Theme:** Learn the plumbing behind Claude's superpowers: **MCP** (how Claude connects to tools and data) and **Skills** (how Claude learns your procedures). Then let Claude run whole tasks for you with **Cowork** and **Claude in Chrome**.
> **Main surfaces:** Claude (chat, Cowork, Desktop extensions), Claude Code for building, and Chrome.
> **Projects:** Paramur (partner acquisition, bookkeeping prep) and Auralis (website QA, brand voice).

← [Week 2](week-2-claude-apps-power-user.md) · [Plan overview](README.md) · [Week 4 →](week-4-claude-code-foundations.md)

---

## Day 15 · Mon: MCP explained, plus your first MCP connection that gets something done

**Goal:** Understand MCP well enough to explain it, then connect a server and produce a real result.
**Time:** ~60 min · **Where:** 🖥️ Claude Code CLI and 💬 Claude · **Cost:** free

### Theory (20 min)
- **The problem.** Every AI app × every tool means endless custom integrations. **MCP (Model Context Protocol)** is the open standard that fixes this. Think of it as "USB-C for AI": any MCP-capable app connects to any MCP server.
  - Anthropic created it in 2024. Since December 2025 it has been governed under the Linux Foundation's **Agentic AI Foundation**.
  - Claude, ChatGPT, VS Code and many others support it. The current spec version is **2026-07-28**.
- **The three roles:**
  - **Host:** the AI app, e.g. Claude or Claude Code.
  - **Client:** one connection inside the host.
  - **Server:** a program that exposes capabilities.
- **What a server offers:**
  - **Tools** are actions Claude can call: *search_emails*, *create_issue*, *take_screenshot*.
  - **Resources** are data and context, e.g. files and records. In Claude Code you can @-mention them.
  - **Prompts** are ready-made templates that appear as commands.
  - **MCP Apps** extension: servers can show **interactive UI** inside Claude. That's how "interactive connectors" work.
- **Transports:**
  - **stdio** is a *local* server process on your computer, with access to local files and apps.
  - **Streamable HTTP** is a *remote* server on the internet, usually with an **OAuth** login.
- **Where MCP appears for you:**
  - claude.ai **connectors** (remote; Gmail, Calendar and Drive are MCP too).
  - **Desktop extensions** (local, `.mcpb`).
  - **Claude Code**, via `claude mcp add` or `.mcp.json`.
  - **Cowork.**
- **Security:**
  - A server can read data and take actions, so install only trusted ones (claude.ai/directory is reviewed).
  - Use least privilege.
  - Treat fetched content as possible **prompt injection**.
  - Keep a human approval step for consequential actions.

### Practice (40 min)
**Path A, Claude Code (local CLI). Your first server in one command.** The official Claude Code documentation server is free and needs no login:
```bash
claude mcp add --transport http claude-code-docs https://code.claude.com/docs/mcp
claude mcp list            # should show: connected
```
Then, in `claude`, *get something done*:
> Using the claude-code-docs MCP server, look up how PreToolUse hooks work. Then produce a ready-to-use hook config and script that blocks Claude from editing .env files and credential files in a Python project. Explain each line.

Save the result for Day 31. You've just used MCP to research and generate a working config.

**Path B, Claude chat:** go to **Customize → Connectors → "+ Add" → "Add custom connector"** and add the same URL (`https://code.claude.com/docs/mcp`). Enable it in a chat and ask *"What's new in Claude Code this month?"*. Watch the tool calls appear. The Free plan allows only one custom connector. If the connector won't connect, stay with Path A, or connect any server from the directory instead to see MCP tool calls in chat.

**Bonus (free GitHub account plus a personal access token):** add GitHub's official MCP server:
```bash
claude mcp add --transport http github https://api.githubcopilot.com/mcp/ --header "Authorization: Bearer YOUR_GITHUB_PAT"
```
Then: *"Read my roadmap notes and create 5 well-written GitHub issues with labels in my Paramur repo. Show them to me before creating."*

### ✅ Done when
- `claude mcp list` shows a connected server, and you produced something useful with it, like the hook config.
- You can explain host, client, server, tools, resources and prompts in your own words.

### 💡 Smart idea
Before building any integration yourself, check whether an MCP server already exists in claude.ai/directory or registry.modelcontextprotocol.io. It usually does.

📖 [MCP quickstart for Claude Code](https://code.claude.com/docs/en/mcp-quickstart) · [Connect Claude Code to tools via MCP](https://code.claude.com/docs/en/mcp) · [MCP specification](https://modelcontextprotocol.io) · [MCP starter pack](cheatsheets/mcp-starter-pack.md)

---

## Day 16 · Tue: Desktop extensions and local MCP: Claude on your own computer

**Goal:** Give Claude safe access to a local folder and get a tedious job done.
**Time:** ~60 min · **Where:** 💬 Claude Desktop (macOS or Windows) · **Cost:** free

### Theory (15 min)
- **Local MCP servers** run on your machine and can work with local files and apps.
  - In Claude Desktop they come as **Desktop extensions** (`.mcpb` bundles): **Settings → Extensions → Browse extensions**, one-click install, with secrets stored in your OS keychain.
  - The older manual route through `claude_desktop_config.json` still works.
- **The Filesystem server** can read, write, move and search files, but **only in the folders you allow**.
- **Cowork** can also work in "trusted folders" directly (Day 19). Today you learn the MCP layer underneath.
- **Safety:** use a dedicated working folder, work on *copies*, and keep "never delete" in the prompt.

### Practice (45 min): bookkeeping prep (Paramur)
1. Create `~/Claude-Workspace/inbox` and **copy** (don't move) 20–30 receipts or invoices (PDFs or photos) into it.
2. Install the **Filesystem** extension, allowing only `~/Claude-Workspace`.
3. Prompt:
   > Organize the files in ~/Claude-Workspace/inbox: create folders by YYYY-MM, rename each file to YYYY-MM-DD_vendor_amount.ext where readable, and create index.csv (date, vendor, net, VAT, gross, category, filename). Never delete anything; list files you couldn't read.
4. Spot-check 3 files against the CSV.

**Auralis alternative:** sort a folder of website and Instagram photos into themes, and create a CSV with suggested alt texts in DE, EN and ES.

### ✅ Done when
- The folder is organized, `index.csv` exists, and 3 spot-checks are correct.

### 💡 Smart idea
Make this a monthly routine before handing documents to your accountant. Later you can automate it with a Cowork scheduled task.

📖 [Local MCP servers and desktop extensions (help center)](https://support.claude.com/en/articles/10949351) · [MCPB format (GitHub)](https://github.com/modelcontextprotocol/mcpb)

---

## Day 17 · Wed: Build your own MCP server (about 40 lines of Python)

**Goal:** Demystify MCP by building, testing and connecting your own server.
**Time:** ~75 min · **Where:** 🖥️ Claude Code (use it to write the code), plus a terminal · **Cost:** free

### Theory (15 min)
- **Anatomy of a server:** a name, plus **tools** (a function, a description and typed parameters), plus optional resources and prompts.
- **Claude reads your tool names and descriptions** to decide when and how to call them, so write them like documentation for a smart colleague.
- **Official SDKs (v2, 2026):**
  - **Python:** the `mcp` package, with `from mcp.server import MCPServer` (it was called `FastMCP` in v1).
  - **TypeScript:** `@modelcontextprotocol/server`.
- **Test** with the **MCP Inspector**, then connect the server to Claude Code with `claude mcp add`, or package it as `.mcpb` for Claude Desktop.
- **Good tool design:**
  - A few high-level tools rather than many tiny ones.
  - Clear names.
  - Concise outputs.
  - Helpful error messages.
  - **Read-only first.**

### Practice (60 min)
In this **Learning** repo (public, so use **public information only**), ask Claude Code:
> Create mcp-servers/auralis-info/server.py using the official Python MCP SDK v2 (MCPServer). Expose read-only tools based on the public facts in Auralis Natura's llms.txt: list_programmes(language), get_programme(name, language), suggest_programme(goal, weeks_available). Include good descriptions and a README with run instructions using uv.

Minimal shape, for reference:
```python
from mcp.server import MCPServer

mcp = MCPServer("auralis-info")

@mcp.tool()
def list_programmes(language: str = "en") -> str:
    """List Auralis Natura programmes with price and duration. language: de, en or es."""
    ...

if __name__ == "__main__":
    mcp.run()  # stdio
```
Then:
1. **Test:** `uv run mcp dev server.py` opens the Inspector. Call each tool.
2. **Connect:** `claude mcp add auralis-info -- uv run --with "mcp[cli]" mcp run /absolute/path/server.py`
3. **Use:** *"Which programme fits someone with low energy who has about 4 weeks?"* Watch Claude call your tool.

### ✅ Done when
- The Inspector lists your tools, and Claude answered a question by calling your server.

### 💡 Smart idea
A **private, read-only Paramur server** (in the private repo) could answer *"What's the status of order X?"* or *"Which partner inquiries are open?"* straight from your data. That's a big time saver, and it stays read-only until you trust it.

📖 [Python SDK](https://github.com/modelcontextprotocol/python-sdk) · [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) · [MCP Inspector](https://github.com/modelcontextprotocol/inspector) · [Writing effective tools for agents](https://www.anthropic.com/engineering/writing-tools-for-agents)

---

## Day 18 · Thu: Agent Skills: package your know-how once, use it everywhere

**Goal:** Create a skill that makes Claude follow your brand voice or process automatically.
**Time:** ~60 min · **Where:** 💬 Claude (Customize → Skills) and 🖥️ Claude Code · **Cost:** included (needs code execution on)

### Theory (15 min)
- **A skill is a folder with `SKILL.md`**: YAML frontmatter with `name` and `description`, then instructions. It can also hold `scripts/`, `references/` and `assets/`.
  - It's an **open standard** (agentskills.io), used by Claude apps, Claude Code, the API and other agent products.
- **Progressive disclosure:**
  1. Name and description (~100 tokens) are always loaded.
  2. The body loads when the skill is relevant. Keep it under ~500 lines.
  3. Extra files load only when needed.

  So you can have dozens of skills without bloating context.
- **Skill vs. Project vs. MCP:**
  - **Project:** workspace context for one business.
  - **MCP:** a connection to tools and data.
  - **Skill:** *how to do something well*, reusable across chats, Cowork, Claude Code and the Office add-ins.

  Best combo: MCP gives access, and a skill teaches how to use it.
- **In Claude:**
  - Built-in skills create Excel, Word, PowerPoint and PDF files.
  - Upload your own as a ZIP under **Customize → Skills → "+"**.
  - On Mac in Cowork you can also **record** a skill by demonstrating a task.
  - Skills enabled in your account sync to Cowork, Claude Code and the Office add-ins.
- **Limits in claude.ai:** name max 64 characters and description max 200. Use only standard frontmatter fields. Claude Code-only fields like `disable-model-invocation` are rejected on upload.
- **Security:** only use skills from trusted sources, and read any bundled scripts.

### Practice (45 min)
Create **`auralis-brand-voice`** (or **`paramur-partner-communication`**):
> Help me write a SKILL.md following the Agent Skills standard. Name: auralis-brand-voice. Description (max 200 chars): when to use it. Body: voice principles, do/don't list, DE/EN/ES glossary of brand terms, compliance checklist (coaching not medical advice; no cure/diagnosis claims; "Dr." = scientific doctorate), and 3 example captions per language.

Save it as `auralis-brand-voice/SKILL.md`, zip the folder, and upload it via Customize → Skills. Test it in a fresh chat **without mentioning the skill**:
> Write an Instagram caption about sleep and energy in German and Spanish.

Check that the skill triggered. Then ask Claude Code in the Auralis repo to use it too, or commit a copy to `.claude/skills/`.

### ✅ Done when
- The skill triggers automatically in at least two surfaces, and the output follows your rules.

### 💡 Smart idea
Good next skills for you:
- Partner offer emails.
- App Store release notes.
- A "health-claims check".
- A monthly report format.
- Your personal "SG quality bar" checklist.

📖 [What are skills (help center)](https://support.claude.com/en/articles/12512176) · [Agent Skills overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) · [Example skills (anthropics/skills)](https://github.com/anthropics/skills) · [Engineering post: Equipping agents with Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)

---

## Day 19 · Fri: Cowork and Claude in Chrome: delegate whole tasks

**Goal:** Hand Claude an outcome rather than a prompt, then come back to finished work.
**Time:** ~60 min · **Where:** 🤖 Cowork (desktop, web or mobile) and Claude in Chrome · **Cost:** included in Pro/Max

### Theory (15 min)
- **Cowork** is the agent architecture of Claude Code, made for **knowledge work** (no terminal).
  - You describe the result you want. It plans, splits work across sub-agents, uses files, connectors and a browser, and delivers **finished files**: spreadsheets with working formulas, decks, documents or organized folders.
  - Tasks run in the **cloud** and keep going when your laptop is closed.
  - Your local **trusted folders**, the built-in browser and computer use are available through the desktop app while it's open.
  - **Scheduled tasks:** `/schedule` or "Scheduled" in the sidebar.
  - You can monitor and steer from your phone.
  - Anthropic is merging Cowork and chat into one Claude, so you may simply see "Claude" doing this.
- **Claude in Chrome** (all paid plans) is a browser agent.
  - It reads, clicks, types, navigates and fills forms with *your* logins, and works across tabs.
  - It runs in the background and notifies you when it's done or needs approval.
  - Save prompts as **shortcuts** (type "/") and schedule them.
- **Built-in guardrails.** Claude in Chrome never makes purchases, creates accounts, handles card or ID data, deletes permanently, or follows instructions found in emails or web pages. It asks before downloads or entering sensitive data.
- **Your safety rules:**
  - Use a **separate Chrome profile** without banking, health or government accounts.
  - Give Cowork a **dedicated working folder**.
  - Start with simple tasks.
  - Stop immediately if Claude drifts.

### Practice (45 min)
1. **Cowork, Paramur partner prospecting:**
   > Research interior-design studios and premium furnishing stores in Vienna, Salzburg and Munich from their public websites. Build an Excel prospect list: name, city, website, style focus, project types, contact page URL, and a fit score 1–5 for a premium AR-wallpaper partnership with a one-line reason. 30 rows. I'll check back later.

   Then review 5 rows yourself.
2. **Chrome, Auralis website QA:**
   > On auralisnatura.com, go through the main pages and the booking/contact flow in German, English and Spanish. Don't submit any form. Report broken links, untranslated text, typos and layout problems in a table.

   Save it as a shortcut `/site-qa`.

### ✅ Done when
- The prospect spreadsheet is ready and plausible, and the QA report exists as a reusable shortcut.

### 💡 Smart idea
Describe the **finished state** ("an Excel with these columns, 30 rows, scored") instead of the steps. That's the mindset shift from chat to agent.

📖 [Get started with Cowork](https://support.claude.com/en/articles/13345190) · [Cowork scheduled tasks](https://support.claude.com/en/articles/13854387) · [Claude in Chrome](https://support.claude.com/en/articles/12012173) · [Use Claude in Chrome safely](https://support.claude.com/en/articles/12902428)

---

## Day 20 · Sat: 🛠️ Build day: your ops autopilot (a scheduled morning brief)

**Goal:** A brief that lands every weekday without you lifting a finger.
**Time:** 90 min · **Where:** 🤖 Cowork scheduled tasks (or a Claude Code routine), with your Gmail, Calendar and Drive connectors

1. **Design the brief.** Turn the format into a small skill or a saved prompt:
   - Today's meetings with a one-line prep each.
   - Emails needing a reply (partners and clients), with Gmail **drafts** prepared.
   - Deadlines in the next 7 days.
   - The top 3 priorities.
   - One "risk or opportunity" line.
2. **Test it manually** twice and refine.
3. **Schedule it:** use `/schedule` (or Scheduled in the sidebar), weekdays at 07:30. If your account offers the **morning brief** skill (`/morning`), try it as a ready-made alternative.
4. **Add one weekly task**, e.g. *"Mondays 08:00: partner pipeline review: new inquiries, offers awaiting reply, suggested follow-ups (drafts only)."*
5. **Check the usage it consumes**, in Settings → Usage.

### ✅ Done when
- The brief arrived on schedule on two days and you tuned it once.

---

## Day 21 · Sun: 🔁 Review and reflect

**Time:** 30 min
1. Quiz:
   1. Host vs. client vs. server?
   2. Tools vs. resources vs. prompts?
   3. stdio vs. Streamable HTTP: which one for a server that reads your local files?
   4. When do you use a skill, a project or an MCP server?
   5. What should Cowork and Chrome *never* get access to in your setup?
   6. Why should tool descriptions be written carefully?
2. 🎓 Free courses in **Claude Academy**: *Introduction to Model Context Protocol*, *Introduction to agent skills*, *Introduction to Claude Cowork* (see [resources](resources.md)).
3. Add your connectors, skills and scheduled tasks to your **AI Playbook** under "My assets".
