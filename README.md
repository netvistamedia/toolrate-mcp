# ToolRate MCP

**An MCP server for developers who can't afford to burn tokens on flaky APIs or oversized LLM calls.**

Wire it into Claude Code, Cursor, Zed, Windsurf — any MCP-compatible editor — and your agent picks up two things it didn't have before:

1. **It knows which APIs are actually reliable right now** — before it calls them and burns a retry.
2. **It picks the cheapest LLM that can still do the job** — Groq or DeepSeek for simple prompts, Claude or GPT-4 only when they're worth the bill.

Both powered by live data from agents using ToolRate in the wild.

## Install in 30 seconds

```bash
# TypeScript (recommended)
claude mcp add toolrate --env TOOLRATE_API_KEY=your_key -- npx -y @toolrate/mcp-server

# Python — if your stack prefers uvx
claude mcp add toolrate --env TOOLRATE_API_KEY=your_key -- uvx toolrate-mcp
```

No key yet? Two options:

- Grab one at [toolrate.ai](https://toolrate.ai) — free, no credit card.
- Or install *without* `TOOLRATE_API_KEY` set. The first tool exposed will be `toolrate_register` — call it with your email and paste the returned key into your MCP config. Zero browser visits.

Works identically with Cursor, Zed, Windsurf, and anything that speaks MCP over stdio. Setup snippets for each editor live in [`typescript/README.md`](./typescript/README.md) and [`python/README.md`](./python/README.md).

## The free tier is actually generous

- **100 assessments a day**, permanently free.
- Scores are cached server-side for ~5 minutes, so checking the same tool twice in a row only burns one quota call.
- Most solo devs building agents never touch the cap. If you do, you're probably already shipping something that deserves a paid tier anyway.

## The deal

ToolRate runs on a simple trade:

- **You help us** — every `toolrate_report` your agent sends after a real call teaches the scoring engine which APIs actually hold up in production. That's the signal nobody scraping docs can get.
- **We help you** — in return you get (a) reliability scores that reflect reality, not marketing pages, and (b) an LLM router that routes simple prompts to a $0.15/M-token model instead of a $15/M-token one. Up to 100× cheaper per token for the easy tasks your agent does most often.

Wire up the guard pattern once and the savings compound quietly behind your agent from then on. The more you report, the sharper the data gets for everyone.

## What's in the box

Nine tools, one API key:

| Tool | What it's for |
|---|---|
| `toolrate_assess` | "Is this API reliable right now?" — score, pitfalls, mitigations, best alternatives. |
| `toolrate_route_llm` | "Cheapest model that can still do this under my budget?" — 7 providers ranked (Anthropic, OpenAI, Groq, Together, Mistral, DeepSeek, Ollama). |
| `toolrate_report` | "Here's what actually happened." — how ToolRate learns. |
| `toolrate_fallback_chain` | "What do other agents switch to when this tool fails?" |
| `toolrate_hidden_gems` | "Which underrated tools punch above their weight?" |
| `toolrate_search_tools` | Search/browse 600+ rated tools. |
| `toolrate_categories` | List canonical categories. |
| `toolrate_my_usage` | Check your daily quota. |
| `toolrate_register` | Bootstrap a new key from inside the MCP client (only exposed when no key is configured). |

Full tool schemas, guard-pattern prompts, and per-editor setup:

- TypeScript → [`typescript/README.md`](./typescript/README.md) — `@toolrate/mcp-server` v0.1.2 on [npm](https://www.npmjs.com/package/@toolrate/mcp-server)
- Python → [`python/README.md`](./python/README.md) — `toolrate-mcp` v0.1.1 on [PyPI](https://pypi.org/project/toolrate-mcp/)

Both expose identical tools and read the same `TOOLRATE_API_KEY` — pick whichever runtime your editor's MCP integration is happier with.

## License

[MIT](./typescript/LICENSE) on both packages — embed in anything, commercial use welcomed. The ToolRate API backend is source-available under [BUSL-1.1](https://github.com/netvistamedia/toolrate).
