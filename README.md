# ToolRouter

The OpenRouter for tools. One MCP connection gives any AI agent 254 hosted tools, pay per call.

This [Agent Plugin](https://agent-plugins.org) connects [Cursor Marketplace](https://cursor.com/marketplace) and Grok Bot to ToolRouter.

**Author:** OUTSIDE HQ LTD  
**Homepage:** [toolrouter.com](https://toolrouter.com)

## What it does

Connect once over MCP. The agent discovers and calls hosted specialist tools: web search, scraping, image and video generation, SEO, finance, property, compliance, and more. Free tools work before an account is claimed. Paid tools are pay per call from $0.005. As of 3 September 2026 the catalog has 254 tools and 1,345 skills; current counts are at [toolrouter.com/tools](https://toolrouter.com/tools).

Nothing in this repository executes catalog tools locally. Calls go to `https://api.toolrouter.com/mcp`.

## Supported countries and users

The hosted gateway is available worldwide over HTTPS. Individual catalog tools may cover only some countries, languages, or data sources. Those limits come from live `discover` results, not from this plugin.

## Installation and authentication

Install **ToolRouter** from Cursor Marketplace or Grok Bot → Plugins, then complete the ToolRouter OAuth screen.

There is no API key in this package. The consent screen can connect without a prior account and provisions a free session. Bare MCP calls without a bearer token return `Authentication required`. Free tools work before the user claims the account. Claiming is required to buy credits, run paid tools, save credentials, or keep history.

Production MCP: `https://api.toolrouter.com/mcp` (Streamable HTTP).

Manual Cursor config, if you are not using the marketplace install:

```json
{
  "mcpServers": {
    "toolrouter": {
      "url": "https://api.toolrouter.com/mcp"
    }
  }
}
```

Setup guides: [Cursor](https://toolrouter.com/docs/connect-cursor), [Grok Bot](https://toolrouter.com/docs/connect-grok-bot), [Grok](https://toolrouter.com/docs/connect-grok).

## Representative prompts

- Use ToolRouter to get the current weather in London. Name the skill and show every field it returned.
- Use ToolRouter to discover a free website check, run it on https://example.com, and return the result.
- Create a ToolRouter file in the plans section named Reviewer Note containing "Cursor marketplace fixture", then read it back.

## MCP tools and permissions

The connection exposes 47 MCP tools. `discover` searches the catalog. `use_tool` runs one catalog skill. Other tools manage the ToolRouter account, files, jobs, connectors, and knowledge.

**Read / discovery**

`account_setup`, `account_list`, `credits_balance`, `credits_usage`, `invoice_list`, `key_list`, `credential_list`, `credential_guide`, `file_list`, `file_read`, `persona_list`, `scene_list`, `product_list`, `outfit_list`, `connector_list`, `job_list`, `job_get`, `discover`, `brain_query`, `brain_status`, `brain_lint`, `brain_expand`, `brain_wings`

**Prepare an action (no charge or send by themselves)**

`account_switch`, `account_preferences`, `subscription_manage` (returns a Stripe URL), `top_up_credits` (returns a Stripe checkout URL), `credential_guide`, `connector_add` (returns an authorization URL when OAuth is required), `feedback_review`, `feedback_debug`, `feedback_request_tool`, `brain_settings` with `action: "get"`

**Commit a write, spend, or destructive change — confirm first**

`use_tool` (catalog execution; may cost money or change upstream data), `key_create`, `key_delete`, `credential_save`, `credential_delete`, `credential_default`, `file_write`, `file_delete`, `connector_remove`, `connector_permissions` with `action: "set"`, `brain_add`, `brain_update`, `brain_delete`, `brain_admin`, `job_cancel`, `account_preferences` with `action: "set"`

The plugin cannot raise the user's ToolRouter permissions. Catalog tools only do what the authenticated account can already do.

## Writes, bookings, messages, and payment

A live tool result is required for prices, availability, connector state, and account balances. Do not invent them.

`top_up_credits` and `subscription_manage` prepare Stripe checkout or portal URLs. Opening the URL is not payment. Do not say a charge, credit top-up, or subscription change succeeded unless ToolRouter or Stripe reports that state after the user finishes checkout.

Do not send messages, publish posts, book appointments, delete files, save secrets, or spend credits unless the user confirmed that action.

## Privacy, terms, support, security

- Privacy: https://toolrouter.com/privacy
- Terms: https://toolrouter.com/terms
- Support: support@toolrouter.com
- Privacy requests: privacy@toolrouter.com
- Vulnerability reports: security@toolrouter.com
- Contact: https://toolrouter.com/contact
- Docs: https://toolrouter.com/docs

This plugin stores no secrets. Review ToolRouter's privacy policy before connecting.

## Local testing

1. Copy this repository to `~/.cursor/plugins/local/toolrouter`.
2. Reload Cursor, or run **Developer: Reload Window**.
3. Open **Customize** and confirm the ToolRouter MCP server and `toolrouter` skill.
4. Complete OAuth if prompted.
5. Ask: `Use ToolRouter to get the current weather in London.`
6. For a reversible write, create then delete a plans-section file with `file_write` and `file_delete`. Do not complete a real Stripe charge to test checkout.

## Files

- `plugin.json` — Agent Plugins 1.0.0
- `mcp.json` — hosted ToolRouter MCP
- `skills/toolrouter/SKILL.md`
- `logo.png` — ToolRouter mark (400×400)
