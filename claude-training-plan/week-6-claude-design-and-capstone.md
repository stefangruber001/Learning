# Week 6: Claude Design, visual work and capstone

> **Theme:** Make Claude your designer: on-brand one-pagers, decks, social assets and interactive prototypes, then hand designs to Claude Code and ship them. The week ends with a capstone that uses everything from the six weeks.
> **Main surfaces:** Claude Design (inside any Claude conversation, or at claude.ai/design), the `/design` and `/design-sync` skills in Claude Code, and Claude Slides.
> **Projects:** Auralis already has a React design system synced to Claude Design. Paramur has a strong brand (logo and brand guide) that's ready to become a design system.

← [Week 5](week-5-claude-code-advanced.md) · [Plan overview](README.md)

---

## Day 36 · Mon: Claude Design fundamentals, and your first design

**Goal:** Understand what Claude Design does and produce a print-ready one-pager.
**Time:** ~60 min · **Where:** 🎨 Claude Design · **Cost:** included in Pro and above (it uses your normal plan limits)

### Theory (20 min)
- **Claude Design** comes from Anthropic Labs. It launched in April 2026 and is still in beta.
- **What you can make:** interactive prototypes, wireframes, mockups, pitch decks, one-pagers, landing pages, marketing and social assets, and even code-powered prototypes (animation, 3D, built-in AI).
- **Where to find it:**
  - Just ask for a design in any conversation, or pick **Output → Design**.
  - The **Artifacts** tab.
  - The standalone app at **claude.ai/design**.
  - **`/design`** in Claude Code.
  - On mobile you can only view designs.
- **What you can give it:** a text brief, screenshots and photos, Word, PowerPoint or Excel files, your codebase, and your **design system**.
- **Four ways to edit:**
  1. **Chat** for structural changes ("make it two columns, move testimonials up").
  2. **Inline comments** on an element for targeted fixes.
  3. **Direct canvas edits:** drag, resize, align, type.
  4. **Adjustment sliders** that Claude creates for spacing, color and size.
- **Export and share:**
  - **Files:** ZIP, PDF, PPTX or standalone HTML.
  - **Send to other tools:** Canva, Adobe, Gamma, Miro, Netlify, Vercel, Wix and others.
  - **Share link:** view, comment or edit access.
  - **Handoff:** send the design to Claude Code.
- ⚠️ **No version history yet.** Export or duplicate before big changes.
- **A one-minute design crash course:**
  - **Hierarchy:** one dominant message.
  - **Whitespace:** leave breathing room.
  - **Contrast:** for readability and accessibility.
  - **Alignment** and **consistency**.
  - **One clear call to action.**
- **A design brief should include:** audience, goal, key message, CTA, format and size, brand, and must-have content.

### Practice (40 min)
**Paramur:** a partner one-pager (A4, German) for interior-design studios. Upload the Paramur logo and 3 product or room photos.
> Design an A4 one-pager for interior-design studios: what Paramur is, how the AR wall preview helps them close sales, the partner process in 4 steps (inquiry → reviewed offer → order → delivery), partner benefits, and contact with a QR code to the partner portal. Premium, calm, lots of whitespace. Use the logo and photos provided.

Iterate: 2 inline comments, 1 slider adjustment, 1 structural chat change. Export as **PDF**.

**Auralis alternative:** a one-pager for the *Connection* corporate workshop, aimed at HR managers (German).

### ✅ Done when
- You have a PDF you'd actually send to a partner or client.

### 💡 Smart idea
Keep a "design brief" prompt in your AI Playbook. Most bad designs come from vague briefs, not from the tool.

📖 [Get started with Claude Design](https://support.claude.com/en/articles/14604416) · [Launch post](https://www.anthropic.com/news/claude-design-anthropic-labs) · [Product page](https://claude.com/product/design)

---

## Day 37 · Tue: Design systems, so every design is on-brand automatically

**Goal:** Connect both brands to Claude Design so you never have to explain your brand again.
**Time:** ~60 min · **Where:** 🎨 Claude Design + 🖥️ Claude Code · **Cost:** included

### Theory (15 min)
- **A design system** holds your brand's *tokens* (colors, type, spacing), *components* (buttons, cards, sections), *assets* (logos, photos) and *rules*.
- **Three ways to create one in Claude Design:**
  1. **From a chat or brand assets:** logos, fonts, existing decks, PDFs, Figma files. Best for **brand** systems, so use this for Paramur.
  2. **From code with Claude Code `/design-sync`:** converts a React design system (tokens and components) and uploads it. Best for **product** systems. Auralis already uses this; authorize first with `/design-login`.
  3. **Migrating** an existing team system in the standalone app.
- **Manage** design systems in **Settings → Design systems**.
- **Keep them in sync.** After changing components in code, run `/design-sync` again. A sync can also uncover real bugs in your shipped CSS.

### Practice (45 min)
1. **Auralis (code-based):** in Claude Code inside the Auralis repo, run `/design-login` (once), then `/design-sync`, to refresh the system after recent changes. Then in Claude Design:
   > Using the Auralis Natura design system, design a 'Which programme fits you?' homepage section, 3 variants, desktop and mobile.

   This connects to your Day 10 quiz artifact.
2. **Paramur (brand-based):** create a design system from the logo, the brand guide and 2–3 existing documents or website screenshots. Test it with:
   > Make an Instagram post announcing a new motif collection.

### ✅ Done when
- Both design systems exist, and a test design looks on-brand without any extra brand instructions in the prompt.

### 💡 Smart idea
One design system then powers **everything**: one-pagers, decks, social posts, landing pages and app screens. That's consistency you'd normally pay an agency for.

📖 [Design systems in Claude Design](https://support.claude.com/en/articles/14604397) · [`/design-sync` in Claude Code](https://code.claude.com/docs/en/commands)

---

## Day 38 · Wed: Decks and documents that look designed

**Goal:** Pick the right tool for presentations and produce a deck you'd really present.
**Time:** ~60 min · **Where:** 🎨 Claude Design, Claude Slides, and the PowerPoint add-in · **Cost:** included

### Theory (15 min)
- **Which tool when:**
  - **Claude Slides:** quick, editable decks; present straight from Claude; export to PPTX or PDF.
  - **Claude Design:** highly visual, brand-system decks and one-pagers; export to PPTX or PDF, or send to Canva.
  - **PowerPoint add-in:** work inside your *existing* corporate template.
  - **`/slides` in Claude Code:** a deck built from repository knowledge, e.g. a release review.
- **Storytelling that works:**
  - Situation → complication → resolution.
  - One message per slide, with the headline *stating* the point.
  - Visuals over bullet lists.
  - Speaker notes for details.

### Practice (45 min): pick one
- **Auralis:** an 8-slide pitch deck for the *Connection* corporate wellbeing workshop, aimed at HR managers, in a DE version and an EN version, using the design system. Export PPTX and PDF.
- **Paramur:** a 6-slide partner pitch.
  1. Problem: end customers can't imagine the wallpaper.
  2. Solution: the AR preview.
  3. Process.
  4. Partner benefits.
  5. Example project.
  6. Next steps.

Ask Claude for speaker notes and a *"tough questions from the audience"* list with answers.

### ✅ Done when
- The exported deck and speaker notes are ready, and you rehearsed it once.

---

## Day 39 · Thu: Prototype to code, from Claude Design to Claude Code

**Goal:** Turn a design into working, verified code on your website.
**Time:** ~75 min · **Where:** 🎨 Claude Design → 🖥️ Claude Code · **Cost:** included

### Theory (15 min)
- **Two routes:**
  1. Design and iterate in Claude Design, then **hand off to Claude Code** (local, or Claude Code on the web) with the full design context.
  2. Start in Claude Code with **`/design <brief>`**. It drafts editable artboards as an artifact, you pick and tweak one, and Claude implements it.
- **Verification is still king:**
  - Check responsive breakpoints (390px and desktop).
  - Check accessibility: contrast, focus states, alt text.
  - Look at real screenshots, via the Playwright MCP from Day 32 or Claude in Chrome.

### Practice (60 min)
**Auralis: ship the programme finder.** Take the Day 37 design (plus the logic from your Day 10 artifact) and hand it off to Claude Code.

In the Auralis repo, in **plan mode**:
> Implement this programme-finder section in the website: DE/EN/ES, use our design-system components and tokens, respect the stylesheet mirror rule, add it to llms.txt if relevant. Show me the plan first.

Then implement on a branch, screenshot it at 390px and 1280px with Playwright, run `/code-review`, and open a PR.

**Paramur alternative:** design and implement an improved "new inquiry" screen for the partner portal or app.

### ✅ Done when
- A PR exists with the implemented design, screenshots attached, and the review passed.

### 💡 Smart idea
The flow is **idea → artifact prototype (Day 10) → designed version (Day 37) → production code (today)**. You validate cheaply first and only build what works.

📖 [Claude Code `/design` skill (What's new, Aug 2026)](https://code.claude.com/docs/en/whats-new/2026-w34) · [Artifacts from Claude Code](https://code.claude.com/docs/en/artifacts)

---

## Day 40 · Fri: Visual content at scale: social media, dashboards and brand consistency

**Goal:** Build reusable templates and a data dashboard so content production takes minutes.
**Time:** ~60 min · **Where:** 🎨 Claude Design + 💬 Claude (artifacts) · **Cost:** included

### Theory (15 min)
- **Template thinking.** Design a format once (carousel, quote card, before/after, announcement) and reuse it with new content. Pair it with a content calendar and your brand-voice prompts or skills.
- **Claude Design builds layouts in code** and uses *your* photos and assets. Use real photography, i.e. Paramur room shots and Auralis portraits, for authenticity.
- **Data-viz basics:**
  - Pick the chart that answers the question.
  - Label directly instead of using legends.
  - One message per chart.
  - No 3D or gimmicks.

  The built-in **dataviz** skill helps with all of this.

### Practice (45 min)
1. **Content system:** ask your Auralis or Paramur project for a 4-week Instagram plan (themes, hooks, CTAs; for Auralis in DE/EN/ES). Then in Claude Design:
   > Using our design system, create 3 reusable Instagram carousel templates: tip carousel, myth vs. fact, client-journey story.

   Export them, or send them to Canva.
2. **KPI dashboard:** create an artifact dashboard from *anonymized* Paramur order data (monthly volume, m², motif mix, inquiry → order conversion). Bonus: connect it to a Google Sheet through your connectors so it updates live.

### ✅ Done when
- You have 3 templates and 1 dashboard that you'll actually reuse.

---

## Day 41 · Sat: 🏆 Capstone: idea → research → design → build → automate → share

**Goal:** Prove to yourself that you can run a complete initiative with Claude.
**Time:** 2–3 h · **Where:** everywhere

**Choose one real initiative:**
- **Auralis:** launch the programme finder as a lead magnet (the website section, an email follow-up, and an Instagram announcement).
- **Paramur:** a partner-acquisition campaign (target list, outreach emails, one-pager, deck, landing section).
- Your own idea from your idea list.

**Checklist. Use at least one tool from each week:**
| Step | Tool (week) | Deliverable |
|---|---|---|
| 1. Research | Research mode (W2) | Cited brief: market, audience, competitors |
| 2. Plan and content | Project + prompting (W1–2) | Plan doc (`/docs`) with messages in all needed languages |
| 3. Design | Claude Design + design system (W6) | One-pager, social templates, section design |
| 4. Build | Claude Code: plan → tests → PR (W4–5) | Merged PR / deployed page |
| 5. Automate | Routine, scheduled task or hook (W3, W5) | e.g. a weekly KPI or broken-link check |
| 6. Share | Artifact or deck (W2, W6) | Status page or pitch for your partner or team |
| 7. Review | `/code-review`, AI-policy check (W1, W4) | No compliance or brand violations |

### ✅ Done when
- The initiative is live or ready to launch, and you can explain which tool did what and why.

---

## Day 42 · Sun: 🎓 Graduation: assess, systematize, continue

**Time:** 60 min
1. **Self-assessment.** Rate each skill 1–5 and pick the 3 lowest for next month:
   - Prompting
   - Verification
   - Projects and memory
   - Artifacts
   - Research
   - Connectors and MCP
   - Skills
   - Cowork and Chrome
   - Claude Code core
   - Hooks, subagents and plugins
   - Automation
   - Claude Design
2. **Your AI Operating Manual (1 page):**
   - Which tool for which job.
   - Your non-negotiable rules (privacy, review, compliance).
   - Your active automations.
   - Your weekly rhythm.

   Keep it in your **private** notes and paste the core into your profile and CLAUDE.md files.
3. In the local CLI, run **`/insights`** again and compare it to Week 4.
4. **30-day continuation plan:**
   - One new automation or skill per week.
   - Monthly memory and rules hygiene.
   - A quarterly research radar.
   - **Stay current:** skim Claude Code's weekly [What's new](https://code.claude.com/docs/en/whats-new/index), the [Claude release notes](https://support.claude.com/en/articles/12138966-release-notes) and the [Anthropic news page](https://www.anthropic.com/news).
5. Celebrate. 🎉 Then pick one Claude Academy course certificate to finish (see [resources](resources.md)).
