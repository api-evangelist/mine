---
generated: '2026-07-20'
method: generated
name: Discover AI agents and their posture (AISPM)
description: Enumerate discovered AI agents and devices for a tenant and read each agent's posture, vulnerabilities, and governance signals.
api: openapi/mine-openapi-original.json
operations:
  - GET /api/aispm/v1/public/agents
  - GET /api/aispm/v1/public/agents/{id}
  - GET /api/aispm/v1/public/agents/{id}/vulnerabilities
  - GET /api/aispm/v1/public/agents/{id}/signals
  - GET /api/aispm/v1/public/devices
source: >-
  Grounded in openapi/mine-openapi-original.json AISPM paths (verified verbatim;
  spec declares no operationIds, so steps cite METHOD + path).
---

# Discover AI agents and their posture (AISPM)

Use this to read MineOS AI Security Posture Management (AISPM) inventory: the AI agents and devices discovered for a tenant and their risk posture.

## Auth
- API-key Bearer: `Authorization: Bearer <APIKey>` over HTTPS. See `authentication/mine-authentication.yml`.
- Use the EU or US endpoint matching your account.

## Steps
1. **List agents** — `GET /api/aispm/v1/public/agents`. Returns every discovered agent with read-time rollups: device count, current posture score, current risk score/level, business-purpose classification. Empty array (never 404) when none discovered yet.
2. **Get one agent** — `GET /api/aispm/v1/public/agents/{id}` for full detail: tools, skills, every device it was found on, business purpose, current risk/posture scores.
3. **Vulnerabilities** — `GET /api/aispm/v1/public/agents/{id}/vulnerabilities` (posture-analysis run findings). Empty list with null run/score when no completed run — never 404.
4. **Signals** — `GET /api/aispm/v1/public/agents/{id}/signals` (governance signals from the insights run). These two risk-factor collections are served separately and are never unioned.
5. **List devices** — `GET /api/aispm/v1/public/devices`; `GET /api/aispm/v1/public/devices/{id}` for one device plus every agent found on it.

## Errors
- Error envelope `{ internalErrorCode, message }`. See `errors/mine-problem-types.yml`. AISPM read endpoints return empty collections rather than 404 when a tenant has no discoveries yet.

## Notes
- Insights rollups: `GET /api/aispm/v1/insights`. Enrollment for device agents is handled by the `/enroll` and `/api/aispm/v1/enrollment-tokens` operations.
