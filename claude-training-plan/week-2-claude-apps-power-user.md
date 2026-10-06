# Week 2: Claude apps power user

> **Theme:** Move from chatting to *working* with Claude: persistent project workspaces, memory, self-built mini-apps, deep research, your Google tools, and Claude inside the documents you already use.
> **Main surfaces:** Claude on the web, desktop and mobile, plus Claude Docs and Slides, and the Excel, PowerPoint and Word add-ins.
> **Projects:** a Paramur HQ and an Auralis HQ, which you'll keep using after this plan.

← [Week 1](week-1-ai-foundations-and-prompting.md) · [Plan overview](README.md) · [Week 3 →](week-3-mcp-skills-and-agents.md)

> ℹ️ **Interface note (October 2026).** Anthropic is merging Chat and Cowork into a single "Claude" without a mode switch, rolling out gradually to Pro and Max. Some menus may look slightly different from what's described here. Look for the **"+" menu**, **Customize** in the sidebar, and **Settings**.

---

## Day 8 · Mon: Projects, your business headquarters

**Goal:** Create one workspace per business that already knows your brand, products and rules.
**Time:** ~60 min · **Where:** 💬 Claude (web or desktop) · **Cost:** included (Free allows only 5 projects)

### Theory (15 min)
- **A Project** has its own **files (knowledge)**, **instructions**, **separate memory** and a project summary. On paid plans, retrieval (RAG) switches on automatically for large knowledge bases, so you can store much more than fits in one chat.
- **Instructions vs. knowledge vs. memory:**
  - **Instructions** say *how to behave*: role, tone, languages, rules. Keep them short and concrete.
  - **Knowledge** is *what to know*: brand guide, offer descriptions, FAQs, process overviews and examples of great past outputs.
  - **Memory** is what Claude *learns over time* in that project.
- **What makes a great project:**
  - One clear purpose.
  - Curated, current documents rather than everything you have.
  - Good examples (example emails, captions, offers).
  - An explicit "never do" list.
- **Not:** secrets, passwords, IBANs, client health data or full customer lists.

### Practice (45 min)
1. **Paramur HQ:**
   - **Upload:** your brand guide, a public product and motif overview, the process overview (inquiry → offer → order → payment, without prices or personal data), the Instagram playbook and 3–5 example emails you like.
   - **Instructions:**
     > You are Paramur's business assistant. Default language German (Austrian business context), English on request. Be concise and premium in tone. Never invent prices, delivery times or legal statements; ask me instead. Partners never see prices before a reviewed offer.
2. **Auralis HQ:**
   - **Upload:** `llms.txt`, which is already an excellent knowledge file, plus the programme descriptions, the tone and brand guide, and FAQs.
   - **Instructions:**
     > Trilingual (DE/EN/ES); warm, evidence-based, never medical advice or promises; "Dr." is a scientific doctorate; always include the coaching disclaimer where appropriate.
3. **Test** each project with 3 real tasks, e.g. *"Answer this partner question…"*, *"Write a newsletter intro…"*, *"Explain the difference between the programmes…"*. Fix the instructions where an answer missed.

### ✅ Done when
- Both projects answer three test prompts correctly in brand voice without extra explanation from you.

### 💡 Smart idea
Add a file called **"Examples of great work"** to each project and update it whenever you get an output you love. Good examples improve results more than longer instructions.

📖 [Projects (help center)](https://support.claude.com/en/articles/9517075)

---

## Day 9 · Tue: Memory, past chats and personalization

**Goal:** Make Claude remember the right things and forget the wrong ones.
**Time:** ~45 min · **Where:** 💬 Claude · **Cost:** included (searching past chats needs a paid plan)

### Theory (15 min)
- **Memory** builds categorized entries from your chats. Manage them in **Settings → Memory → Topics**: view, edit, delete, pause or reset.
  - Project memory is kept separate from your general memory.
  - Sensitive categories aren't saved unless you opt in.
  - To keep a single chat out of memory, switch off **Memory** in the **"+" menu** before your first message, or use an **incognito chat** (the ghost icon).
- **Search and reference past chats** (paid plans): *"What did we decide about the partner discount last month?"*
- **Import memory** from ChatGPT or Gemini: **Settings → Memory → Start import**. Anthropic gives you a prompt to run in the other assistant.
- **Layers of personalization:**
  - **Profile preferences** apply to every chat.
  - **Memory** holds learned facts.
  - **Project instructions** apply per workspace.
  - **Skills** cover reusable procedures and styles (Week 3).

  Anthropic is moving the older "Styles" feature to skills.
- **Settings → Reflect** gives a monthly recap of how you use Claude.

### Practice (30 min)
1. **Settings → Memory:** read every topic. Delete anything wrong or outdated, and add the essentials (your two businesses, languages, working style).
2. Ask:
   > What do you know about me and my work? What seems outdated or missing? Ask me 5 questions to improve it.
3. Ask *"Find the chat where we created the partner onboarding guide and continue it"*.
4. If you used another AI before, try **memory import**.
5. Do one **incognito** chat and confirm it doesn't appear in history.

### ✅ Done when
- Your memory is accurate and short, and you've used past-chat search once.

### 💡 Smart idea
Put a 5-minute "memory hygiene" check on your calendar once a month, together with Settings → Reflect.

📖 [Memory and chat search](https://support.claude.com/en/articles/11817273) · [Memory import](https://support.claude.com/en/articles/12123587) · [Incognito chats](https://support.claude.com/en/articles/12260368)

---

## Day 10 · Wed: Artifacts, or building tools and apps without code

**Goal:** Build and share a small interactive tool for one of your businesses.
**Time:** ~60 min · **Where:** 💬 Claude (web or desktop) · **Cost:** included

### Theory (15 min)
- **An artifact** is a standalone piece of work Claude builds next to the chat: a web page, calculator, quiz, dashboard, diagram, document or game. They're saved in the **Artifacts** tab.
  - Highlight part of one and choose **"Edit with Claude"** to change only that section.
  - Artifacts need "Code execution and file creation" switched on in Settings → Capabilities.
- **Templates** (beta, paid): Docs, Slides and Design.
- **AI-powered artifacts:** the artifact can call Claude itself, e.g. a caption generator. People who use it sign in, and **their own plan pays for their usage**, not yours.
- **Paid-plan superpowers:**
  - Artifacts can **use your connectors** (live data).
  - They can **store data** (up to 20 MB, personal or shared). This is enough for checklists, mini-CRMs and polls.
- **Sharing:** artifacts are private by default. You can share by link or invite by email.

### Practice (45 min): pick one
- **Auralis: "Which programme fits you?"**
  - A 5-question quiz that recommends Clarity, Change or Balance.
  - DE/EN/ES switch, brand colors, a CTA to book the free intro call.
  - Compliant wording: coaching, not diagnosis.
- **Paramur: "Wall-area and panel estimator"** for partners.
  - Several walls and windows → m², waste %, panel count.
  - No prices, matching your inquiry-first process.
  - Saves past calculations (storage).

Iterate three times: function → design → edge cases. Then share the link and test it on your phone.

### ✅ Done when
- The artifact works on mobile, and one other person tried it and gave feedback.

### 💡 Smart idea
Artifacts are perfect **prototypes**. Validate the idea with real users first. In Week 6, Claude Code builds the production version into your website.

📖 [Artifacts (help center)](https://support.claude.com/en/articles/17153992) · [Share artifacts](https://support.claude.com/en/articles/9547008)

---

## Day 11 · Thu: Research and web search, your analyst team

**Goal:** Produce a cited, decision-ready research report and verify it.
**Time:** ~60 min · **Where:** 💬 Claude · **Cost:** included (Research needs a paid plan)

### Theory (15 min)
- **Web search** (all plans) handles quick facts and current information. **Web fetch** reads a URL you paste.
- **Research** (paid) runs a multi-step investigation for several minutes across many sources. It can include your connected Gmail, Calendar and Docs, and returns a **cited report**.
  - Start it from **"+" → Research** or type **`/deep-research`**.
- **Brief research like a consultant:**
  - The decision it informs.
  - Scope: region, time frame, segment.
  - Sources to prefer or avoid.
  - Output format: tables, ranking, recommendations.
  - What would change your mind.
- **Verify.** Open at least 3 citations, check dates, and ask *"What's the strongest evidence against this conclusion?"*

### Practice (45 min): pick one
- **Paramur:**
  > Research the premium and AR wallpaper market and interior-design partner programmes in Austria and Germany (2025–2026). Top 10 competitors with pricing model, partner conditions, channels and visualization tools. End with 5 concrete opportunities for Paramur, ranked by impact.
- **Auralis:**
  > Research online holistic-health and nutrition coaching in the DACH region and Spain (2025–2026): positioning, price ranges, client acquisition channels, and the legal rules for health claims and professional titles. End with 5 differentiation opportunities for a science-based coach, plus compliance risks to avoid.

### ✅ Done when
- You have a cited report, 3 verified sources, and one decision or action you'll take from it.

### 💡 Smart idea
Save your best research brief as a template. Rerun it quarterly ("what changed since last time?") to get a competitive radar for free.

📖 [Research (help center)](https://support.claude.com/en/articles/11088861) · [Web search](https://support.claude.com/en/articles/10684626)

---

## Day 12 · Fri: Connectors: Gmail, Calendar, Drive and the directory

**Goal:** Let Claude work with your real tools, safely and with you approving every action.
**Time:** ~60 min · **Where:** 💬 Claude (your Gmail, Calendar and Drive connectors are already connected) · **Cost:** free

### Theory (15 min)
- **Connectors give Claude tools and data.** They're built on **MCP** (Model Context Protocol), which you'll study on Day 15.
- **Where to find them:**
  - **Customize → Connectors** or **claude.ai/directory**: Gmail, Calendar, Drive, Google Docs, Sheets and Slides (beta), Notion, Canva, Figma, Asana, Slack, and many more.
  - **Interactive connectors** show live UI inside the chat.
- **Control.** You authorize each connector (OAuth) and choose per tool whether Claude may act or must ask. Claude asks before sending or sharing.
- **Risk:** emails and documents may contain *prompt-injection* text. Rules: least privilege, drafts instead of sends, and a human click for anything external.

### Practice (45 min)
1. **Inbox triage:**
   > Search my Gmail from the last 7 days for partner inquiries and client requests. Make a table: sender (initials only), topic, urgency, suggested next step. Create Gmail **drafts** (don't send) for the top 3, in the right language and brand voice.

   Run it inside the Paramur or Auralis project, so the brand rules apply.
2. **Week planning:**
   > Look at my Google Calendar for next week and propose three 60-minute focus blocks for my Claude training, avoiding early mornings.

   Create the events only after you approve.
3. **Drive:** *"Find my latest brand or price document in Drive and summarize what changed versus the previous version."*
4. **Directory:** browse it and connect one more free connector that fits your work, e.g. Canva for social graphics or Notion if you use it.

### ✅ Done when
- 3 good drafts are waiting in Gmail (not sent), and your focus blocks are in the calendar.

### 💡 Smart idea
Make *"Create drafts, never send"* a project instruction. You keep 100% control and still save most of the typing.

📖 [Connectors](https://support.claude.com/en/articles/11176164) · [Google Workspace connectors](https://support.claude.com/en/articles/10166901)

---

## Day 13 · Sat: 🛠️ Build day: Claude where you already work (Docs, Slides and Office)

**Goal:** Use Claude's document tools and the Office add-ins on a real planning task.
**Time:** 90 min · **Where:** 💬 Claude, Claude Docs and Slides, and the Excel, PowerPoint and Word add-ins · **Cost:** included in Pro

### Theory (15 min)
- **Claude Docs** (beta, paid) are living documents that you co-write with Claude and others.
  - Start one with **`/docs`**.
  - Mention **@Claude in a comment** to ask for an edit.
  - Export to Word, PDF, Markdown or Google Docs.
- **Claude Slides** (beta, paid) lets you edit slides directly, present from Claude, and export to PowerPoint or PDF.
- **Claude for Excel, PowerPoint and Word** (generally available on Pro; install "Claude for Microsoft 365" from Microsoft AppSource):
  - **Excel:** cell-level citations, edits that keep your formulas intact, and fixes for errors like #REF!.
  - **PowerPoint:** builds slides in your own template.
  - **Word:** edits as **tracked changes**.
- **Claude for Google Workspace** (beta, launched October 2026) is a sidebar in Google Docs, Sheets and Slides.

### Practice (75 min)
1. **Q4 plan (Claude Docs):** `/docs Create "Q4 2026 plan" for Paramur and Auralis: goals, 3 initiatives each, owners, dates, risks`. Refine two sections through @Claude comments.
2. **Deck (Claude Slides):** turn the plan into a 6-slide deck and export it as PPTX.
3. **Excel (add-in), on a copy, never on the live workbook:** open a *copy* of a Paramur workbook and ask Claude to explain the structure, find formula errors, and add a summary sheet with clear formulas. Check the tracked cells.

### ✅ Done when
- The plan doc, the exported deck, and an improved Excel copy exist, and you know which tool you'd use for what.

---

## Day 14 · Sun: 🔁 Review, plus voice and mobile

**Time:** 30 min (take a walk)
1. **Voice mode on your phone:** on a 15-minute walk, brainstorm with Claude by voice: *"Help me think through how to get 10 new interior-design partners for Paramur by spring."* Afterwards, ask for a written summary with next steps.
2. **Phone shortcuts:**
   - iOS: the Claude widget, *"Ask Claude"* via Siri or the Share menu, and the Action button.
   - Android: the home-screen widget.
   - Mac: double-tap **Option** for **quick entry** from any app.
3. Quiz:
   1. Instructions vs. knowledge vs. memory in a project: what goes where?
   2. How do you keep one sensitive chat out of memory?
   3. Who pays for usage when someone uses your AI-powered artifact?
   4. Web search vs. Research: when do you use which?
   5. Why "drafts, never send" with connectors?
4. 🎓 Continue the AI Fluency course and add your best prompts of the week to your **AI Playbook**.
