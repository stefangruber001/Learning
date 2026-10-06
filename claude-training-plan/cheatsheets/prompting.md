# Prompting cheat sheet

Based on Anthropic's prompt-engineering guidance. Works in Claude chat, Projects, Claude Code, Cowork and Claude Design.

## The 8 fundamentals
1. **Clear and direct:** write for a brilliant colleague with zero context.
2. **Context:** who it's for, why, what good looks like, constraints.
3. **Examples:** 2–5 varied examples of the output you want.
4. **Structure:** separate material from instructions with tags like `<document>`, `<context>`, `<instructions>`.
5. **Role:** "You are an experienced …"
6. **Room to think:** "Think through the options first, then answer."
7. **Output spec:** length, format, language, tone. Say what *to do*, not only what to avoid.
8. **Long documents:** put the documents first and the question last, and ask for quotes before the answer.

## Universal template
```
ROLE: You are …
GOAL: I need … so that …
CONTEXT: <context> audience, background, why it matters </context>
INPUT: <document> … </document>
CONSTRAINTS: must / must not …
FORMAT: length · structure · language(s) · tone
EXAMPLES: <example> … </example>
QUALITY BAR: It's great if …
If anything is unclear, ask me before you start.
```

## Power phrases
| Situation | Say this |
|---|---|
| You lack clarity | "Interview me one question at a time until you have what you need." |
| Important decision | "Give me 3 options with trade-offs and your recommendation." |
| Quality check | "Grade this 1–10 against: clarity, accuracy, brand fit, length. Then fix the weakest point." |
| Blind spots | "What am I not asking that I should be?" |
| Stress test | "Argue against this as a skeptical customer, competitor or lawyer." |
| Facts | "Only use the attached documents. Quote the passage for each claim. Say 'not in the documents' if missing." |
| Uncertainty | "How confident are you? What would change your answer? How can I verify it?" |
| Reuse | "Write a reusable prompt that would produce this result for other topics." |
| Iteration | "Keep the structure. Make it 30% shorter, warmer, and remove the jargon." |
| Translation and localization | "Localize (don't just translate) for Austrian / German / Spanish readers; keep the brand terms unchanged." |

## Prompt chains for bigger work
- **Content:** research → outline → draft → critique against a rubric → final → 3 headline variants
- **Decision:** facts → options → criteria → scoring table → recommendation → risks
- **Code (Claude Code):** explore → plan (plan mode) → tests → implement → verify → review → commit

## Claude Code prompt pattern
```
Goal: <what and why>
Context: read <files/dirs> first. Related: <issue/PR/screenshot>
Constraints: don't touch <x>; keep <convention>; languages DE/EN/ES
Verify: run <tests/command>; for UI, screenshot at 390px and 1280px
Process: start in plan mode, ask questions, then implement on a new branch
Done when: <verifiable condition>
```

## Common mistakes
- Vague goal ("make it better") → say *better for whom, measured how*.
- No examples for style-sensitive tasks.
- One giant chat for everything → start new chats per topic, carry over a summary.
- Accepting the first output → iterate with precise feedback.
- Trusting numbers, laws or quotes without checking the source.
- Pasting secrets or client personal or health data → anonymize first.
