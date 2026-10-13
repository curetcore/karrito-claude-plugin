# Karrito for Claude

Karrito is an online store builder for small businesses, with checkout over WhatsApp. This plugin
lets you work with your Karrito store from a conversation in Claude: browse your catalog, review
orders and customers, check inventory and read your store reports.

## What it includes

- **One connector**, `https://karrito.app/api/mcp`, Karrito's own MCP server. You sign in with
  your own Karrito account through OAuth.
- **27 workflow skills** that teach Claude how Karrito works, including products, variants and inventory,
  categories, orders, customers, discounts, shipping, reviews, pages, navigation, theme, team,
  connections, CSV import and export, and analytics.

## How it handles your data

- The plugin sends requests only to `https://karrito.app`. It contains no other servers, hooks,
  scripts or packages.
- Claude only sees stores your Karrito account can already manage. Your current role and plan
  still decide what is allowed.
- Sensitive changes are never applied by Claude alone: Claude prepares the exact change, and you
  approve it on a Karrito page before it is applied.
- It does not process payments and does not operate the point of sale.

Privacy policy: <https://karrito.app/privacy> · Terms: <https://karrito.app/terms> ·
Support: <https://karrito.app/contact>

## Examples

- "Show me the products in my store."
- "Summarize my store sales for the last seven days."
- "Show the connections configured for my store."

## Requirements

A Karrito account with at least one store. Available actions depend on the tools your connection
exposes, your role in the store and the store's plan.
