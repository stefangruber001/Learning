# MCP starter pack

These are free or free-tier MCP servers to try, with the exact commands. They were checked against official READMEs and docs in October 2026; MCP spec version 2026-07-28.

## Where MCP lives in your setup
| Surface | How to add a server | Notes |
|---|---|---|
| **Claude (chat, Cowork)** | Customize → Connectors → directory, or "+ Add" → "Add custom connector" (remote URL) | The Free plan allows 1 custom connector. The server must be reachable from the internet |
| **Claude Desktop (local)** | Settings → Extensions → Browse extensions (`.mcpb` one-click) | Secrets go in the OS keychain |
| **Claude Code CLI** | `claude mcp add …` | Scopes: `local` (default, just you, this project) · `project` (writes `.mcp.json`, shared) · `user` (all your projects) |
| **Claude Code cloud sessions** | Commit `.mcp.json` (project scope) to the repo, or enable claude.ai connectors on the session | Servers added at local or user scope aren't available in the cloud |

**Syntax (Claude Code):**
```bash
claude mcp add --transport http <name> <url>                 # remote server
claude mcp add <name> -- <command> [args...]                  # local (stdio) server
claude mcp add --scope project ...                            # share via .mcp.json
claude mcp list | claude mcp get <name> | claude mcp remove <name>
/mcp                                                          # inside a session: status, OAuth login
```

## Good first servers
| Server | Command (Claude Code) | Account / cost | Try this |
|---|---|---|---|
| **Claude Code Docs** | `claude mcp add --transport http claude-code-docs https://code.claude.com/docs/mcp` | none, free | "How do I write a Stop hook? Give me a ready config." |
| **Playwright** (browser) | `claude mcp add playwright -- npx -y @playwright/mcp@latest` | none (Node 18+) | "Screenshot my site at 390px and list layout issues." |
| **GitHub** (official, remote) | `claude mcp add --transport http github https://api.githubcopilot.com/mcp/ --header "Authorization: Bearer YOUR_GITHUB_PAT"` | free GitHub account + personal access token | "Create issues from my roadmap notes (show me first)." |
| **Context7** (up-to-date library docs) | `claude mcp add --scope user --transport http context7 https://mcp.context7.com/mcp --header "Authorization: Bearer YOUR_API_KEY"` | free key recommended | "Use the latest Flask docs to …" |
| **Hugging Face** | `claude mcp add hf-mcp-server -t http "https://huggingface.co/mcp?login"` | free account (anonymous tools without one) | "Find a small open model for German text classification." |
| **Notion** | `claude mcp add --transport http notion https://mcp.notion.com/mcp` | Notion account (OAuth) | "Turn this meeting note into a Notion task list." |
| **Figma** | `claude mcp add --transport http figma https://mcp.figma.com/mcp` | Figma account. ⚠️ Starter plan: very few tool calls per month | "Implement this frame as HTML/CSS." |
| **Sentry** | `claude mcp add --transport http sentry https://mcp.sentry.dev/mcp` | Sentry account (OAuth) | "What are the top errors this week?" |

**Official reference servers** (for learning; local, stdio). They live in the `modelcontextprotocol/servers` repo:

| Server | Command | Account / cost | Try this |
|---|---|---|---|
| **Filesystem** | `claude mcp add filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Claude-Workspace` | none | "Organize this folder" |
| **Fetch** | `claude mcp add fetch -- uvx mcp-server-fetch` | none. ⚠️ It can reach local network addresses | "Fetch this page and summarize it." |
| **Git** | `claude mcp add git -- uvx mcp-server-git --repository /abs/path/repo` | none | "Explain the last 10 commits." |
| **Memory** | `claude mcp add memory -- npx -y @modelcontextprotocol/server-memory` | none | A knowledge-graph memory |
| **Time** | `claude mcp add time -- uvx mcp-server-time` | none | Time-zone conversions |
| **Everything** | `claude mcp add everything -- npx -y @modelcontextprotocol/server-everything` | none | A test server showing all MCP features |

> Browse more: the **reviewed** directory at [claude.ai/directory](https://claude.ai/directory) and the **official registry** at [registry.modelcontextprotocol.io](https://registry.modelcontextprotocol.io).

## Build your own (Python SDK v2)
```bash
uv init my-server && cd my-server && uv add "mcp[cli]"
```
```python
# server.py
from mcp.server import MCPServer      # v1 name was FastMCP

mcp = MCPServer("demo")

@mcp.tool()
def add(a: int, b: int) -> int:
    """Add two numbers."""
    return a + b

if __name__ == "__main__":
    mcp.run()                          # stdio
```
```bash
uv run mcp dev server.py                                                     # test in MCP Inspector
claude mcp add demo -- uv run --with "mcp[cli]" mcp run /abs/path/server.py  # connect to Claude Code
```
TypeScript: `npm install @modelcontextprotocol/server zod`, then test with `npx @modelcontextprotocol/inspector npx tsx src/index.ts`. To ship a local server to Claude Desktop as a one-click extension: `npm i -g @anthropic-ai/mcpb && mcpb init && mcpb pack`.

## Safety checklist before connecting any server
- [ ] Is it from a source you trust (official vendor, Anthropic directory, or code you've read)?
- [ ] Does it need write access? Start **read-only** where possible.
- [ ] Is access limited to the folders, repos or workspaces it needs?
- [ ] Could it fetch untrusted content (web, email)? Then expect **prompt injection**, and keep approvals on.
- [ ] Are secrets in environment variables or the keychain, never in committed files?
- [ ] Do you know how to disconnect it? (`claude mcp remove`, or the Connectors settings)
