# toolrouter

Discover and run ToolRouter tools through one MCP connection for web search, scraping, SEO research, image and video generation, audio, company and economic data, and supported connected-account actions including X and LinkedIn posting. Use when ToolRouter is connected or the user chooses it for an external task.

Publisher contact: **blake@humanleap.com**. Public source is maintained in the Humanleap GitHub organisation.

## Install the skill

```bash
pnpm dlx skills add Humanleap/agent-skills --skill toolrouter
```

### Use-case skills

Install one when the job is already known. Each one uses the same ToolRouter connection.

| Skill | Jobs |
|---|---|
| `social-media-scraper` | Profiles, posts, videos, comments, search and trends from TikTok, Instagram, YouTube, X, Facebook, LinkedIn, Reddit, Threads, Bluesky and Pinterest. |
| `ad-library-scraper` | Competitor ads from the Meta Ad Library, Google Ads Transparency Center, LinkedIn, TikTok and Reddit. |
| `ecommerce-scraper` | Product pages from any store plus listings from eBay, Vinted, Facebook Marketplace, Gumtree and other marketplaces. |

```bash
pnpm dlx skills add Humanleap/agent-skills --skill social-media-scraper
```

## Claude Code

```text
/plugin marketplace add Humanleap/toolrouter-agent-plugin
/plugin install toolrouter@toolrouter-agent
```

## Other clients

- Cursor: `.cursor-plugin/plugin.json` and its MCP config.
- Grok Build: `.grok-plugin/plugin.json` and its MCP config; a marketplace review is separate from this source package.
- Gemini CLI: `gemini extensions install https://github.com/Humanleap/toolrouter-agent-plugin`.
- Portable agents: root `plugin.json` and `mcp.json`. A public package is not proof of official store approval.
- Other MCP clients: connect the Streamable HTTP endpoint `https://api.toolrouter.com/mcp`.

## Access and network

Client authentication and provider/account requirements depend on the selected operation. Paid tools consume credits.

This instruction/configuration package has no hooks, shell server, bundled runtime, post-install script or hidden background process. It calls the product endpoint above through the client's MCP integration. Additional providers, payment or delivery destinations are used only for an authorised product workflow described in the skill.

## Skill layout

Following the Postiz agent packaging pattern, the canonical root `SKILL.md` is mirrored byte-for-byte at `skills/toolrouter/SKILL.md`. Both use installation, hard rules, authentication, core workflow, essential tools, common patterns, supporting resources, gotchas and a quick reference. This copies the packaging/workflow formula, not Postiz-specific operations. The homepage is inside frontmatter `metadata` for strict skill-validator compatibility.

Company-wide discovery collection: https://github.com/Humanleap/agent-skills.

License: MIT. Product service terms and pricing still apply.
