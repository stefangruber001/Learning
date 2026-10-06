# Week 1: AI foundations and prompting

> **Theme:** Understand what you're working with: how language models think, where they fail, and how to communicate so you get expert-level output on the first or second try.
> **Main surface:** Claude chat (claude.ai web, the desktop app, or mobile).
> **Projects:** real tasks from Paramur and Auralis, with anonymized data only.

[Plan overview](README.md) · [Week 2 →](week-2-claude-apps-power-user.md)

---

## Day 1 · Mon: How large language models actually work

**Goal:** Build an accurate mental model of AI so you know when to trust it and how to steer it.
**Time:** ~50 min · **Where:** 💬 Claude chat · **Cost:** free

### Theory (20 min)
- **Next-token prediction at huge scale.** A large language model (LLM) is trained on enormous amounts of text to predict the next *token*. A token is a piece of a word, about ¾ of an English word; German and Spanish use a few more tokens per word. Further training (human feedback and Anthropic's constitution-based methods) turns the raw model into a helpful, honest assistant.
- **Training vs. inference.** Training happens once and is very expensive. Inference is every time you chat. The model **doesn't learn from your chat** in real time. Features like Projects, Memory and connectors *re-insert* information into the conversation.
- **The context window is working memory.** It holds everything the model sees at once: system instructions, your messages, files, tool results and the answer itself.
  - The newest Opus, Sonnet and Fable models handle up to **1M tokens**. Haiku 4.5 handles 200K, roughly 500 book pages.
  - Beyond the window, nothing exists for the model.
  - More isn't automatically better: recall degrades as the window fills ("context rot"), so give Claude *relevant* material, not everything.
- **Knowledge cutoff.** The model's built-in knowledge stops at its training date. For anything recent (prices, laws, competitors, software versions), turn on **web search** or give it documents.
- **Probabilistic output.** The same prompt can produce different answers, so regenerate or ask for alternatives when quality matters.
- **Hallucinations** are fluent but false statements. They're most likely with niche facts, exact numbers, quotes, citations, legal details and recent events. You'll learn countermeasures on Day 5.
- **The Claude model family (October 2026):**
  - **Haiku 4.5:** fast and light.
  - **Sonnet 5.5:** the balanced everyday workhorse, on every plan.
  - **Opus 5.5:** deep reasoning for complex, long or agentic work, on Pro and above.
  - **Fable 5.1:** the top tier. ⚠️ On Pro it's billed as extra usage credits; on Max it's included.

  The **model menu** next to Send has three controls: **model**, **effort** (Low → Max) and **thinking**. Newer models always think before answering hard questions. Higher effort and bigger models use more of your plan's usage limits, so match the model to the task.

### Practice (30 min)
1. **Set up your cockpit** on claude.ai → **Settings**:
   - **Profile:** your name, what you do (founder of Paramur and Auralis Natura, builder), and your preferences (language, tone, "be direct, give me options with trade-offs").
   - **Privacy:** at claude.ai/settings/data-privacy-controls, decide whether your chats may be used for model training. If you allow it, data is kept up to 5 years; if not, 30 days. Incognito chats are never used for training.
   - **Capabilities:** see what you can switch on (web search, memory, code execution and file creation, …).
   - Install the **desktop app** (claude.ai/download) and the **mobile app**.
2. **Model comparison.** Ask the same question to **Haiku 4.5**, **Sonnet 5.5** and **Opus 5.5**. Skip Fable on Pro, because it costs extra.
   > Explain how an augmented-reality wallpaper preview works to a 65-year-old interior-design shop owner, in 80 words, in German.

   Compare speed, quality and tone. Which would you use for what?
3. **Cutoff test.** With web search **off**: *"What's your knowledge cutoff? What were the biggest AI announcements last month?"* Then **on**: same question. Notice the difference, and how the model signals uncertainty.

### ✅ Done when
- You can explain *token, context window, knowledge cutoff, hallucination* to a friend in two sentences each.
- Profile, privacy and capability settings are set deliberately.

### 💡 Smart idea
Put your most important standing preferences into your profile once (language rules, the DE/EN/ES needs of your businesses, your tone). Every chat starts better without repeating yourself.

📖 [Anthropic: Claude models overview](https://platform.claude.com/docs/en/about-claude/models/overview) · [How to use Claude (help center)](https://support.claude.com)

---

## Day 2 · Tue: Prompting fundamentals

**Goal:** Learn the techniques behind 80% of great results.
**Time:** ~50 min · **Where:** 💬 Claude chat · **Cost:** free

### Theory (20 min)
Anthropic's prompting guide boils down to:
1. **Be clear and direct.** Treat Claude like a brilliant new colleague with *zero* context. Golden rule: if a colleague would be confused by your prompt, Claude will be too.
2. **Give context.** Who is it for, why does it matter, what does "good" look like, and what are the constraints?
3. **Show examples** (multishot). Two to five varied examples beat long descriptions of style.
4. **Structure with XML-style tags**, e.g. `<context>…</context>`, `<document>…</document>`, `<instructions>…</instructions>`, so instructions and material don't blur.
5. **Give a role.** "You are an experienced B2B sales manager for premium wall coverings in Austria…"
6. **Let it think.** For complex tasks, ask it to reason step by step or weigh options before answering.
7. **Specify the output:** length, structure, language, tone and format (table, bullets, email). Say what to do rather than only what *not* to do.
8. **Long documents:** put the documents first and the question last, and ask for relevant quotes before the answer.

**Reusable template:**
```
ROLE: You are …
GOAL: I need … so that …
CONTEXT: <context> who / why / background </context>
INPUT: <document> … </document>
CONSTRAINTS: must / must not …
FORMAT: length, structure, language(s), tone
EXAMPLES: <example> … </example>
QUALITY BAR: It's great if …
```

### Practice (30 min): before and after
Write each task first as a one-line "naive" prompt, then with the template. Compare.
- **Paramur:** a reply to a new partner asking about conditions. It must stay friendly and price-free at the inquiry stage, and invite them to submit an inquiry via the portal.
- **Auralis:** an Instagram caption for the *Clarity* programme in DE, EN and ES, written as coaching, never as a medical promise.
- **Personal:** an email to plan a meeting with three busy people.

### ✅ Done when
- You have three before/after pairs and can name at least six prompting techniques without looking.

### 💡 Smart idea
When an output is 80% right, don't rewrite it yourself. Tell Claude *exactly* what's wrong ("too salesy; shorter; keep the second paragraph") and let it revise. Your feedback is the prompt.

📖 [Prompt engineering overview](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview) · [Interactive prompt engineering tutorial (free, GitHub)](https://github.com/anthropics/prompt-eng-interactive-tutorial)

---

## Day 3 · Wed: Advanced prompting: conversations, not one-shots

**Goal:** Use multi-step patterns that produce expert-level work.
**Time:** ~50 min · **Where:** 💬 Claude chat · **Cost:** free

### Theory (15 min)
- **Interview me.** Say *"Before you write anything, interview me one question at a time until you have what you need."* Claude pulls out the context you didn't know you had to give.
- **Prompt chaining.** Split big tasks into steps: research → outline → draft → critique → final. Review between steps.
- **Rubrics and self-critique.** Ask *"Grade this draft 1–10 against these criteria, then improve the weakest part."*
- **Meta-prompting.** Ask *"Write the best possible prompt for this task"*, then use and refine it.
- **Perspectives.** Try *"Argue against this"*, *"Act as a skeptical customer"* or *"Red-team this offer."*
- **Conversation hygiene.** Edit an earlier message to branch, or retry for alternatives. Start a **new chat** when the topic changes, because long, messy chats dilute attention. Carry over a short summary.

### Practice (35 min)
Pick one:
- **Paramur:** "Partner onboarding guide", one page. What a new interior-design partner needs to know: process, timelines and who to contact.
- **Auralis:** "Your first two weeks with Auralis Natura", one page for new clients.

Steps:
1. Use the **interview pattern** to create v1.
2. Use a **rubric** (clarity, warmth, completeness, brand fit, length) to get v2.
3. **Meta-prompt:** *"Write a reusable prompt that would produce a document like this for other topics."* Save it.

### ✅ Done when
- You have a polished one-pager plus a reusable prompt you'd actually use again.

### 💡 Smart idea
Ask *"What questions should I be asking that I'm not?"* at the end of important chats. It's one of the highest-value sentences you can type.

📖 [Chain complex prompts](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/chain-prompts) · [Let Claude think](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/chain-of-thought)

---

## Day 4 · Thu: Files, images and data: Claude as analyst and document factory

**Goal:** Turn files and screenshots into analysis and into finished Excel, Word, PowerPoint or PDF files.
**Time:** ~60 min · **Where:** 💬 Claude chat · **Cost:** included in your plan

### Theory (15 min)
- **Uploads.** Claude reads PDFs, Office documents, CSV/XLSX, images and screenshots, and understands charts, tables, handwriting and UI screenshots.
- **Code execution and file creation.** Once enabled in *Settings → Capabilities*, Claude can run code in a sandbox to analyze data, make charts and **create real files**: spreadsheets with working formulas, documents, presentations and PDFs.
- **Accuracy habits:**
  - Ask for **formulas, not pasted numbers**.
  - Ask it to show its method.
  - Spot-check two numbers yourself.
  - Ask *"What assumptions did you make about the data?"*
- **Privacy.** Anonymize before uploading. Remove names, emails, IBANs and any client health information.

### Practice (45 min)
1. **Paramur:** export an *anonymized* inquiries or orders sheet. Delete or replace names and contact data first.
   > Analyze this: monthly volume, average m² per order, top motifs, conversion from inquiry to order. Create an .xlsx with a clean data tab, a summary tab using formulas, and one chart, plus a one-page PDF summary for me.
2. **Auralis:** screenshot the homepage on your phone and upload it.
   > Act as a conversion-focused UX reviewer for a premium coaching brand. List the top 7 improvements, ranked by impact versus effort.
3. **Bonus:** photograph a handwritten note or whiteboard and turn it into a structured to-do list with deadlines.

### ✅ Done when
- You downloaded a Claude-made spreadsheet with working formulas and verified two numbers by hand.

### 💡 Smart idea
Recurring reports (monthly sales, Instagram stats, bookings) are perfect for this. Save the prompt and redo the report every month with fresh data in two minutes.

📖 [Create and edit files with Claude (help center)](https://support.claude.com) · [Vision docs](https://platform.claude.com/docs/en/build-with-claude/vision)

---

## Day 5 · Fri: Trust but verify: hallucinations, privacy and responsible AI

**Goal:** Know the limits, protect your data and your clients, and build a verification habit.
**Time:** ~60 min · **Where:** 💬 Claude chat (with web search) · **Cost:** free

### Theory (25 min)
- **The AI Fluency "4D" framework**, from Anthropic's free course:
  - **Delegation:** deciding *what* to hand to AI, and how.
  - **Description:** communicating goals, context and constraints clearly.
  - **Discernment:** critically evaluating outputs and the AI's behavior.
  - **Diligence:** using AI responsibly, transparently and accountably.
- **Fighting hallucinations:**
  - Provide source documents and ask Claude to *quote* them.
  - Turn on web search or Research for facts.
  - Ask *"How confident are you, and what would change your answer?"*
  - Verify numbers, laws and quotes at the primary source.
  - Allow *"I don't know"* explicitly.
- **Prompt injection.** Web pages, emails and documents can contain hidden instructions aimed at the AI. This matters most when Claude can *act* (connectors, browser, code). Keep a human approval step before anything is sent, paid, published or deleted.
- **Privacy and compliance:**
  - Health information is *special-category data* under the GDPR (Auralis clients). Never paste it into a chat unless you've cleared that legally. Anonymize.
  - Partner pricing, IBANs and contracts (Paramur) also need care.
  - Know your data and training setting, use **incognito chats** for sensitive one-offs, and keep the AI policy below.
- **Marketing rules.** AI can write health or performance claims that are illegal to use, so a human always checks the final wording.

### Practice (35 min)
1. **Fact-check drill.** Ask without web search, then with web search, and then verify one claim on an official site:
   - **Paramur:** *"What are the current e-invoicing requirements for B2B and B2G invoices in Austria, and which formats are accepted?"*
   - **Auralis:** *"Who may legally call themselves a nutritionist in Spain, and what may a health coach say in marketing?"*
2. **Your AI use policy (1 page).** Have Claude interview you, then draft. Cover what never goes into AI, which tasks always need human review, disclosure rules, approved tools and where outputs are stored. Save it privately, not in the public Learning repo.

### ✅ Done when
- You caught at least one inaccuracy or outdated claim, and your one-page AI policy exists.

### 💡 Smart idea
Add a standing instruction to your profile or Projects: *"If you're not sure, say so and tell me how to verify it."* It changes behavior noticeably.

📖 [AI Fluency course (Claude Academy, free)](https://academy.claude.com) · [Reduce hallucinations](https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/reduce-hallucinations) · [Privacy center](https://privacy.claude.com)

---

## Day 6 · Sat: 🛠️ Build day: your prompt library v1

**Goal:** Ten reusable, tested prompts that save you time every week.
**Time:** 90 min · **Where:** 💬 Claude chat

1. List your 10 most frequent writing and thinking tasks, for example:
   - **Paramur:** partner reply, offer follow-up, Instagram post, supplier email, process documentation.
   - **Auralis:** client welcome, programme description, workshop proposal, newsletter, FAQ answer.
2. For each one, use the Day 2 template plus one example of a *great* output.
3. Test each prompt twice and refine it.
4. Store them in one place. Next week they move into **Projects** and later become **Skills**.

### ✅ Done when
- 10 prompts are tested and stored. Bonus: ask Claude to turn the list into an interactive "prompt picker" artifact. That's a preview of Day 10.

---

## Day 7 · Sun: 🔁 Review and reflect

**Time:** 30 min
1. Quiz:
   1. Why doesn't Claude "remember" yesterday's chat by default?
   2. Three techniques that reduce hallucinations?
   3. What goes first in a long-document prompt, the document or the question?
   4. What are the 4 Ds?
   5. Why is prompt injection more dangerous when Claude has tools?
2. 🎓 Start the free **AI Fluency: Framework & Foundations** course in Claude Academy (see [resources](resources.md)).
3. Start your **AI Playbook** (template in the [README](README.md#your-ai-playbook)): your best prompts, lessons and rules.
