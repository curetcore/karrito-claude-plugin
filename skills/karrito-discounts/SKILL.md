---
name: karrito-discounts
description: Create, inspect and control Karrito discount codes, scheduled starts, activation and storefront coupon visibility through prepare/execute workflows the merchant confirms. Use for merchant discount requests.
---

# Karrito Discounts

## Connected surface
The shared tool list includes read tools and legacy API-key writes; this guide's prepare/execute and CSV/handoff workflows are available only when your connection lists them. Check the listed tools before proceeding: this guide by itself does not mean a tool is available. If the approved workflow is missing, stop the write; never fall back to a legacy write or to credentials.


Resolve the authorized store and actual discount IDs. list_discounts defaults active; explicitly request inactive/all as needed. get_discount reads owned records including inactive. Interpret amounts in store currency and percentages as PERCENTAGE, not a fixed amount. Ask for type/value/time boundaries when ambiguous; do not infer a public promotion from an internal coupon request.

Use available prepare_discount_create/update/delete and execute_discount_* workflows. Explicit startsAt and expiresAt are UTC ISO timestamps; display timezone clearly. Effective persisted dates matter in a partial edit: start must not exceed expiration. A newly requested nonnull scheduled start requires KRT-CAT-020 entitlement; legacy unclassified plans fail closed. startsAt=null explicitly clears a schedule. publicoEnTienda explicitly controls coupon display; omission preserves and never silently publishes. isActive is separate from storefront display. usedCount is read-only; never fabricate redemption, checkout activation or a campaign.

Read current type/value before partial editing. Existing limits, billing and role gates remain authoritative. Show the exact payload, confirm it with the merchant, execute the stored handle using a stable key within 5 minutes, and report immutable receipt separately from cache/provider effects. A stale preview requires a new preparation. Do not bypass unavailable prepare/execute tools with legacy raw writes, provider credentials or admin actions.

For multiple actions use available execute_discount_ACTION_batch with at most20 independently prepared handles and stable unique keys. Report per-action results with atomic=false, preserve successes and retry exact original keys. Do not assert global rollback, external delivery or storefront freshness based on REQUESTED/PENDING cache state.

Examples: “20% next weekend” -> clarify timezone and exact start/end, confirm intended public display, then preview. “Hide coupon from the store” -> publicoEnTienda=false, not inferred deletion or deactivation. “Reset uses” -> refuse unsupported redemption mutation. This guide by itself does not mean a tool is available.
