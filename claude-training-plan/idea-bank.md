# Idea bank: smart ways to use Claude in your work

Pick ideas from here for build days, the capstone, and the 30 days after the plan. Each idea names the main tool. ⚠️ means it involves personal or sensitive data, so anonymize it or keep a human approval step.

## Paramur (B2B partners, AR wallpaper, order-to-cash)
| # | Idea | Main tool |
|---|---|---|
| 1 | **Partner inquiry co-pilot:** classify new inquiry emails and draft price-free first replies in German | Connectors (Gmail) + Project |
| 2 | **Offer follow-up radar:** a weekly list of offers sent but not answered, plus friendly follow-up drafts | Connectors + scheduled task |
| 3 | **Partner one-pager and pitch deck** in the Paramur design system | Claude Design |
| 4 | **Wall-area and panel estimator** for partners (no prices) | Artifact → website (Claude Code) |
| 5 | **"What's new" release notes** generated from git history in DE/EN | Claude Code skill |
| 6 | **Weekly health check:** tests, outdated packages, open issues → one GitHub issue | Routine |
| 7 | **Security gate:** `/security-review` and a protect-files hook for anything touching logins, invoices or payments | Claude Code |
| 8 | **Docs index:** consolidate the many guides into one map with outdated or duplicate flags | Claude Code subagents |
| 9 | **Excel sanity check** on a *copy* of the order workbook: formula errors, a summary sheet | Claude for Excel ⚠️ |
| 10 | **Competitor and market radar**, rerun quarterly | Research |
| 11 | **Instagram content system:** monthly plan, carousel templates, captions in brand voice | Project + Claude Design |
| 12 | **Receipts → bookkeeping prep:** a folder of receipts → a structured expense table for your accountant | Cowork ⚠️ |
| 13 | **Partner FAQ assistant:** an AI-powered artifact that answers process questions from your public docs | Artifact |
| 14 | **Website QA:** mobile screenshots, broken links, SEO basics on every release | Playwright MCP / Claude in Chrome |

## Auralis Natura (coaching, DE/EN/ES, design system, iOS app)
| # | Idea | Main tool |
|---|---|---|
| 15 | **"Which programme fits you?"** quiz as a lead magnet | Artifact → Claude Design → Claude Code |
| 16 | **Translation QA agent:** consistency, tone and compliance across DE/EN/ES | Claude Code subagent |
| 17 | **Health-claims guard:** flag wording that sounds like diagnosis, cure or a medical promise | Skill or hook + human review |
| 18 | **Workshop pitch deck** for HR managers (*Connection* programme) | Claude Design / Slides |
| 19 | **Newsletter engine:** monthly topic → article → social snippets in 3 languages | Project + skill |
| 20 | **Client welcome and onboarding pack** (templates, no client data) | Claude Docs |
| 21 | **Lean instructions:** slim the big CLAUDE.md into a core file plus scoped rules | Claude Code (`/doctor prompt-audit`) |
| 22 | **Design-system sync after every UI change**, with an automatic mirror-rule check | `/design-sync` + hook |
| 23 | **AI-search readiness:** keep `llms.txt`, FAQs and structured data current for AI assistants | Claude Code + Research |
| 24 | **App Store release helper:** release notes, screenshots checklist, metadata in 3 languages | Skill + your appbuilder agent |
| 25 | **Content calendar artifact** with storage so you can tick off published posts | Artifact (storage) |

## You as founder (productivity and learning)
| # | Idea | Main tool |
|---|---|---|
| 26 | **Morning brief:** today's calendar, important emails, open tasks, in a 2-minute read | Scheduled task / routine + connectors |
| 27 | **Voice brainstorm on walks**, auto-summarized into next steps | Mobile voice mode |
| 28 | **Weekly review:** what got done, what's stuck, top 3 for next week | Project + Calendar |
| 29 | **Decision memos:** options, criteria, scoring, risks for every big decision | Prompt chain |
| 30 | **Meeting prep:** research the person or company and draft an agenda and questions | Research + Calendar |
| 31 | **Personal plugin marketplace** with your best agents, skills and hooks for every new product | Claude Code plugins |
| 32 | **"Clone for a new product" playbook:** turn your existing build experience into a reusable kickoff | Skills + subagents |
| 33 | **Learning sprints:** have Claude build a quiz artifact from any course or document you read | Artifact |
| 34 | **Travel and events planning** with the Booking.com and Calendar connectors (drafts, no booking without you) | Connectors |
| 35 | **Monthly "AI Playbook" update:** new rules from repeated corrections | Your AI Playbook |

## Rules for every idea
1. **Start small:** one workflow, one week, then measure the time saved.
2. **Human in the loop** for anything sent, published, paid or deleted.
3. **Anonymize** client and partner personal data; never put health data into prompts without a legal basis.
4. **Turn what works into assets:** prompt → skill → plugin; manual → scheduled.
