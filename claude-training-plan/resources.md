# Free learning resources

Checked October 2026. Everything here is free. Items that need a paid API key are marked ⚠️.

## Courses: Claude Academy (free, with badges)
**[academy.claude.com](https://academy.claude.com)** replaces the former Anthropic Academy on Skilljar, and old certificates can be imported. Sign in with your Claude account. Course titles may change, so use the site's search.

| When | Course | Fits |
|---|---|---|
| Week 1 | **AI Fluency: Framework and foundations** (the 4D framework) · **AI capabilities and limitations** · **Claude 101** | Foundations |
| Week 1–2 | **AI Fluency for small businesses** | Applying AI to Paramur and Auralis |
| Week 3 | **Introduction to Model Context Protocol** · **Introduction to agent skills** · **Introduction to Claude Cowork** | MCP, Skills, Cowork |
| Week 4 | **Claude Code 101** · **Claude Code in action** | Claude Code basics |
| Week 5 | **Introduction to subagents** · **Model Context Protocol: Advanced topics** · **The AI-native SDLC playbook** | Advanced Claude Code |
| Optional | **Building with the Claude API** · **Claude Platform 101** | ⚠️ Practicing needs API credits |

**Inside Claude Code:** run **`/powerup`** for interactive lessons with animated demos (local CLI).

## The AI Fluency "4D" framework (by Rick Dakan and Joseph Feller, with Anthropic)
- **Delegation:** setting goals and deciding whether, when and how to engage with AI.
- **Description:** describing goals effectively to prompt useful AI behaviors and outputs.
- **Discernment:** accurately assessing the usefulness of AI outputs and behaviors.
- **Diligence:** taking responsibility for what we do with AI and how we do it.

## Official docs (bookmark these)
| Topic | Link |
|---|---|
| Claude help center (apps, plans, features) | https://support.claude.com |
| Claude app release notes | https://support.claude.com/en/articles/12138966-release-notes |
| Claude Code docs | https://code.claude.com/docs |
| Claude Code weekly "What's new" | https://code.claude.com/docs/en/whats-new/index |
| Claude Code best practices | https://code.claude.com/docs/en/best-practices |
| Claude Code prompt library | https://code.claude.com/docs/en/prompt-library |
| Prompt engineering overview | https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview |
| Prompting best practices | https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices |
| Reduce hallucinations | https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/reduce-hallucinations |
| Models overview | https://platform.claude.com/docs/en/about-claude/models/overview |
| Agent Skills overview | https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview |
| MCP (spec, guides) | https://modelcontextprotocol.io |
| Claude Design: get started | https://support.claude.com/en/articles/14604416 |

## Anthropic engineering articles (deep, free, highly recommended)
| Article | Read in |
|---|---|
| [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) | Week 3 / 5 |
| [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) | Week 4 |
| [Writing effective tools for agents](https://www.anthropic.com/engineering/writing-tools-for-agents) | Week 3 (Day 17) |
| [Equipping agents for the real world with Agent Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) | Week 3 (Day 18) |
| [Code execution with MCP](https://www.anthropic.com/engineering/code-execution-with-mcp) | Week 3 |
| [Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) | Week 6 / after |

## Hands-on repositories
- **[Prompt engineering interactive tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial).** Nine chapters, from basic structure to complex prompts. Reading it is free. ⚠️ Running the notebooks needs an API key, and you must change the model ID from the retired `claude-3-haiku-20240307` to `claude-haiku-4-5`.
- **[anthropics/skills](https://github.com/anthropics/skills).** Example skills and the document skills, a great template source. In Claude Code: `/plugin marketplace add anthropics/skills`.
- **[Claude Cookbook](https://github.com/anthropics/claude-cookbooks).** Recipes for agents, tools, RAG, skills and evals. ⚠️ Needs an API key to run.
- **[MCP servers (reference)](https://github.com/modelcontextprotocol/servers)** · **[Python SDK](https://github.com/modelcontextprotocol/python-sdk)** · **[TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)** · **[MCP Inspector](https://github.com/modelcontextprotocol/inspector)**

## Staying current (10 minutes a week)
1. Claude Code **What's new** (weekly digest), or `/release-notes` in the CLI.
2. Claude **release notes** in the help center.
3. The [Anthropic news page](https://www.anthropic.com/news) and the [Claude blog](https://claude.com/blog).
4. Ask Claude itself, with web search on: *"What changed in Claude, Claude Code and Claude Design in the last 2 weeks that matters for a founder who builds websites, apps and business automation?"*

## Free vs. paid at a glance (Pro plan)
| Included in Pro | ⚠️ Costs extra (usage credits / API) |
|---|---|
| Chat, Projects, memory, Research, artifacts, connectors, skills, Claude Docs and Slides, Office add-ins, Cowork, Claude in Chrome, Claude Design, Claude Code (CLI, Desktop, web, mobile), routines, GitHub Actions with `claude setup-token` | Fable models on Pro, fast mode, `/ultrareview` after 3 free runs, Claude API and Agent SDK with an API key, running the API tutorials and cookbooks |
