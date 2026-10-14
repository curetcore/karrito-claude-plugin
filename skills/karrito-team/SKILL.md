---
name: karrito-team
description: Read Karrito team roles and permissions and guide exact merchant-confirmed team operations without exposing invitations or changing ownership.
---
# Karrito team
Use when a merchant asks about members, roles, pending invitations or changing team access.

## Read saved state
Select the user's intended store explicitly; never use another store as fallback. Call `get_store_team` with the selected `storeId`, limit 1–100 (default 50) and offset (default 0). Members and pending invitations are independent collections ordered by ID, with separate totals; advance offset to cover both. Returns IDs/roles and expiry only: no emails, invitation tokens, bearer links or proof of sending/delivery. Expired invitations are not pending. Static rolePermissions describe Karrito policy; they do not grant permissions or establish who the current user is. Store membership and API entitlement must be current. Denied or unavailable is not an empty team.

## Team change workflow
`prepare_team_action` and `execute_team_action` are available only when your connection lists them; this guide by itself does not mean they are available. Never simulate them using a broad API write, SQL, browser click or unrelated tool.
Prepare one exact existing target: `change-role` (ADMIN or STAFF), `revoke-member` or `cancel-invitation`. Review store, action, target ID/current role and intended new role with the human. Confirm the exact change with the merchant; no execution before that confirmation, and within 5 minutes of preparing. Use returned handle and one stable idempotencyKey. Same-key replay returns its original receipt only after current authorization; another key is not a retry. A stale target/role, changed actor, expired handle or denied access requires a fresh preparation, not a silent retry. Cache PENDING means intent saved, not UI refresh delivered.

## Authority boundaries
OWNER/self changes and ownership transfer are excluded. ADMIN cannot promote or modify ADMIN. OWNER may change ADMIN/STAFF or revoke them with explicit confirmation. A pending invitation cancellation needs its own exact confirmation; cancellation does not revoke an existing member. Never interpret `read` or `stores:read` as mutation permission. Private changes also require existing `store:write`, current `team:manage`, plan and target checks.

## Native workflows
Invite/resend and transfer ownership remain in Karrito's native team screen. Do not create or send invitations, expose tokens/links, infer delivery, transfer billing responsibility, rotate secrets or invent grants. Return a short factual outcome distinguishing prepared, confirmed and executed.
