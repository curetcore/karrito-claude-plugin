---
name: karrito-connections
description: Inspect saved Karrito connection configuration and guide native service setup without exposing credentials or claiming provider verification.
---
# Karrito connections
Use when a merchant asks which external services are configured or why a saved connection appears paused or partial.
Choose the intended store explicitly. `get_store_connections` returns SAVED_CONFIGURATION, Karrito state and current plan availability. `full` is a stored configuration state, not live delivery, OAuth, receiving traffic or current provider health. A stored Meta degraded marker remains historical evidence; no new provider health query is performed. `mcp`/`llaves` reflect active saved API-key configuration, not a marketplace installation or successful OAuth. Webhooks state reflects saved entries, including paused entries, so inspect active flags separately.
Explain off/paused/partial/degraded using the returned hint; do not invent missing credentials or overwrite configuration. Current plan availability and configured state are distinct. Denied/unavailable is not off. If multiple stores are possible, request the choice instead of changing store silently.
Use `list_store_webhooks` and `list_store_webhook_logs` for redacted existing configuration/outcomes. No raw destination, API key, secret, response or payload is exposed. Never infer delivery or downstream processing from saved configuration. For URL, OAuth, API-key issuance, secret creation/rotation or service setup, guide the merchant to Karrito's native connections screen. Do not call provider APIs, fetch configured destinations, send a test or expand grants.
Webhook mutation tools are available only when your connection lists them; read tools alone do not mean a write is available. Summarize saved evidence and the concrete native next step, without claiming a working external connection.
