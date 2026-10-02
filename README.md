<p align="center"><a href="https://lognorm.com"><img src="assets/lockup.svg" alt="LogNorm" width="260"></a></p>

# LogNorm MCP server

**Hand your growth backlog to agents.** [LogNorm](https://lognorm.com) finds what's holding a website's growth back, ranks it, and lets AI agents such as Claude Code, Codex and Cursor do the work next to your team: fixes in your repo, posts with images, research. LogNorm re-checks every fix on the live site and measures what moved.

This repo holds the connection details, the LogNorm agent skill and a Claude Code plugin manifest for the hosted LogNorm MCP server.

| | |
|---|---|
| **Endpoint** | `https://lognorm.com/api/mcp` |
| **Transport** | Streamable HTTP (remote) |
| **Auth** | OAuth 2.1 with dynamic client registration and PKCE. No API keys in prompts or config |
| **Pricing** | Free plan available. Agents run on your own Claude or Codex plan |
| **Docs** | https://lognorm.com/docs/agents |

## What agents can do with it

- **Fix:** read the site audit and GEO/AI-readiness audit (broken pages, metadata, indexing, AI-crawler access, llms.txt, structured data), fix the cause in your codebase, open a PR, then `validate_fix` so LogNorm re-checks the affected pages on the live site.
- **Write:** research briefs from the pages that rank, drafts in your voice, generated covers and diagrams, editor feedback loops.
- **Plan:** topics and hub-and-spoke clusters, and a ranked weekly plan of "moves" shared by people and agents.
- **Research:** keyword lookup and ideas, search volume and difficulty, competitors and the pages they win with, Google Search Console data.
- **Get cited:** track how ChatGPT, Gemini and Google AI Overviews answer your buyers' prompts and turn the gaps into moves.
- **Leave a trail:** every claim, comment, draft and fix shows on the LogNorm dashboard under the agent's name.

Tools include `search`, `execute`, `claim_move`, `create_move`, `plan_move`, `update_move`, `validate_fix`, `start_run`, `research_brief`, `save_brief`, `save_draft`, `generate_image`, `plan_topic`, `keyword_lookup`, `add_competitor`, `add_ai_prompts`, `brain_add` and more. Workflows are exposed as MCP prompts: `weekly_growth`, `growth_review`, `fix_audit`, `write_post`, `plan_topic`, `ai_visibility`.

## Connect

The quickest route: paste this into your agent and it sets itself up.

```
Connect to LogNorm: follow https://lognorm.com/connect.md
```

### Claude Code

```bash
claude mcp add --transport http --scope user lognorm https://lognorm.com/api/mcp
```

Then run `/mcp`, pick **lognorm**, **Authenticate**, and click **Allow** in the browser. Or install this repo as a plugin (MCP server + skill):

```bash
/plugin marketplace add lognorm/lognorm-mcp
/plugin install lognorm@lognorm
```

### OpenAI Codex

```bash
codex mcp add lognorm --url https://lognorm.com/api/mcp
codex mcp login lognorm
```

### Cursor

`~/.cursor/mcp.json`:

```json
{ "mcpServers": { "lognorm": { "url": "https://lognorm.com/api/mcp" } } }
```

### Claude (desktop or claude.ai)

Settings → Connectors → **Add custom connector** → `https://lognorm.com/api/mcp` → Connect → Allow.

### Any other MCP client

Add a remote Streamable HTTP server named `lognorm` with URL `https://lognorm.com/api/mcp`. It answers 401 with OAuth metadata, so clients that support MCP authorization start the sign-in themselves.

## Agent skill

[`skills/lognorm`](skills/lognorm/SKILL.md) holds LogNorm's playbooks (fix audit issues, write posts, plan topics, run growth reviews). It contains instructions only, no credentials. Copy it into `~/.claude/skills`, `~/.agents/skills` or `~/.cursor/skills`, or download https://lognorm.com/api/agents/skill.zip. Skill index: https://lognorm.com/.well-known/agent-skills/index.json

## People without agents

Everything agents can do is also in the LogNorm web app for people, and API keys are available for scripts. Start free at https://lognorm.com/sign-up.

## License

The skill and docs in this repo are MIT licensed. The LogNorm service is governed by its [Terms of Service](https://lognorm.com/terms).
