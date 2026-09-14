---
name: toolrouter
description: Discover and call hosted specialist tools through ToolRouter MCP. Use when the user asks for ToolRouter, live web data, scraping, SEO, images, video, leads, research, or other work that needs a current catalog tool rather than a guessed answer.
---

Use ToolRouter MCP at `https://api.toolrouter.com/mcp` over Streamable HTTP. This plugin contains no API key. The host completes OAuth. Free catalog tools can run before the user claims an account. Paid tools, saved credentials, API keys, and recoverable history need a claimed account with credits.

ToolRouter is a hosted catalog. Geography, price, and availability come from live `discover` results for the selected catalog tool. Do not invent them. Catalog size as of 3 September 2026: 254 tools and 1,345 skills.

## Workflow

1. Call `discover` with the task, an exact tool name, or `*`.
2. Pick the narrowest matching catalog tool and skill. Built-in MCP tools (`discover`, `credits_balance`, `file_write`, and the rest of this plugin's MCP list) are not catalog tools; call them directly, never through `use_tool`.
3. Call `use_tool` with the exact `tool`, `skill`, and schema-valid `input` from discovery.
4. If the response has a `job_id`, poll `job_get` until completed, failed, or cancelled.
5. Return the live result, including asset URLs. Do not substitute training data for a tool result.

If `use_tool` asks for `brain_context`, call `brain_query` first and pass that text at the top level of `use_tool`.

## Confirmation before writes, bookings, messages, or checkout

Ask the user before any of these, unless they already named that exact action:

- A catalog call where `discover` shows a price above $0
- `top_up_credits` or `subscription_manage` (these return a Stripe URL; they do not take payment)
- `key_create`, `key_delete`
- `credential_save`, `credential_delete`, `credential_default`
- `connector_add`, `connector_remove`, `connector_permissions` with `action: "set"`
- `file_delete`, `file_write` with `mode: "update"`
- `brain_delete`, `brain_admin`, material `brain_update`
- `job_cancel`
- `account_switch` or `account_preferences` with `action: "set"`

A Stripe checkout or portal URL is not payment. Do not say credits were added, a subscription changed, or a charge succeeded unless ToolRouter or Stripe state says so after the user completes checkout.

A prepared catalog result is not a sent message, published post, booked appointment, or completed purchase. Connector writes need the user's authorized connector. Give claim or OAuth URLs to the user; never ask for their password or paste secrets into chat.

## Errors

If a tool fails, report the error. Do not retry a cost-bearing call unless the response proves it was not billed or the user authorizes another attempt.
