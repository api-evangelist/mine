---
generated: '2026-07-20'
method: generated
name: Subscribe to MineOS webhooks
description: Register a webhook endpoint and manage event subscriptions to receive MineOS platform events.
api: openapi/mine-openapi-original.json
operations:
  - GET /api/Webhooks/Configurations
  - POST /api/Webhooks/Subscribe
  - POST /api/Webhooks/Endpoint
  - PATCH /api/Webhooks/Subscribe/{id}
  - DELETE /api/Webhooks/Unsubscribe/{id}
source: >-
  Grounded in openapi/mine-openapi-original.json Webhooks paths (verified
  verbatim; spec declares no operationIds, so steps cite METHOD + path) and the
  webhook catalog in asyncapi/mine-webhooks.yml.
---

# Subscribe to MineOS webhooks

Use this to receive MineOS events (e.g. ticket/request lifecycle) at your own endpoint.

## Auth
- API-key Bearer: `Authorization: Bearer <APIKey>` over HTTPS. See `authentication/mine-authentication.yml`.
- Use the EU or US endpoint matching your account.

## Steps
1. **Set the endpoint** — `POST /api/Webhooks/Endpoint` to register the URL MineOS will POST events to. For local development, tunnel with ngrok.
2. **Subscribe to events** — `POST /api/Webhooks/Subscribe` to create a subscription; `PATCH /api/Webhooks/Subscribe/{id}` to update one.
3. **Review configurations** — `GET /api/Webhooks/Configurations` (all) or `GET /api/Webhooks/Configurations/{id}` (one).
4. **Tear down** — `DELETE /api/Webhooks/Unsubscribe/{id}` to remove a subscription; `DELETE /api/Webhooks/Endpoint` to disable the endpoint.

## Errors
- Error envelope `{ internalErrorCode, message }`. See `errors/mine-problem-types.yml`.

## Notes
- See `asyncapi/mine-webhooks.yml` for the event/webhook catalog and payload shapes.
