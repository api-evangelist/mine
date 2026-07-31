---
generated: '2026-07-20'
method: generated
name: Handle a data subject privacy request (DSR)
description: Create, triage, annotate, and close a data subject / privacy rights request (ticket) in MineOS.
api: openapi/mine-openapi-original.json
operations:
  - POST /api/ticket/Create/v2
  - GET /api/ticket/List
  - GET /api/ticket/{ticketId}
  - POST /api/ticket/AddNote
  - POST /api/ticket/CloseV2
source: >-
  Grounded in openapi/mine-openapi-original.json (paths verified verbatim; this
  spec declares no operationIds, so steps cite METHOD + path) and the
  cross-cutting rules in conventions/mine-conventions.yml,
  errors/mine-problem-types.yml, authentication/mine-authentication.yml.
---

# Handle a data subject privacy request (DSR)

Use this to intake and work a privacy rights request (access, deletion, opt-out, etc.) end to end.

## Auth
- API-key Bearer: `Authorization: Bearer <APIKey>`. See `authentication/mine-authentication.yml`.
- All calls must be HTTPS; plain HTTP fails.
- Target the datacenter hosting your account: EU `https://api.portal.saymine.com/` or US `https://api.us.portal.saymine.com/`. See `lifecycle/mine-lifecycle.yml`.

## Idempotency
- There is **no** `Idempotency-Key` header contract. MineOS instead de-duplicates request creation within a ~1-minute window keyed on email + request type, so a retried create inside that window will not spawn a duplicate ticket. See `conventions/mine-conventions.yml` — do not rely on client-controlled idempotency.

## Steps
1. **Create the request** — `POST /api/ticket/Create/v2`. Provide the data subject email and request type. Capture the returned ticket id.
2. **List / find requests** — `GET /api/ticket/List` to browse the queue (cursor pagination via `CursorTokens`; note closed requests drop out of list responses after 3 months).
3. **Inspect one request** — `GET /api/ticket/{ticketId}` for detail, `GET /api/ticket/{ticketId}/log` for its activity log.
4. **Annotate** — `POST /api/ticket/AddNote` to record handling notes; `POST /api/ticket/{ticketId}/require-attention` to flag it.
5. **Close** — `POST /api/ticket/CloseV2` once fulfilled. To bulk-intake use `POST /api/ticket/CreateMany`; to automate fulfillment use `POST /api/ticket/EngageAutopilot/{ticketId}`.

## Errors
- Error envelope is `{ internalErrorCode, message }`. See `errors/mine-problem-types.yml`.

## Notes
- Pagination is cursor-based (`before`/`after` tokens plus `offset`/`limit`). See `conventions/mine-conventions.yml`.
