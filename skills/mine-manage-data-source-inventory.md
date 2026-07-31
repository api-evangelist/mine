---
generated: '2026-07-20'
method: generated
name: Manage the data-source inventory
description: List, inspect, add (catalog or custom), and update data-source systems in the MineOS data map.
api: openapi/mine-openapi-original.json
operations:
  - GET /api/public-v1/system/List
  - GET /api/public-v1/system/{id}
  - POST /api/public-v1/system/AddCatalogSystem
  - POST /api/public-v1/system/AddCustomSystem
  - PATCH /api/public-v1/system/{id}
source: >-
  Grounded in openapi/mine-openapi-original.json (paths verified verbatim; spec
  declares no operationIds, so steps cite METHOD + path); conventions in
  conventions/mine-conventions.yml and data-model/mine-data-model.yml.
---

# Manage the data-source inventory

Use this to build and maintain the company data map (the systems/data sources MineOS inventories).

## Auth
- API-key Bearer: `Authorization: Bearer <APIKey>` over HTTPS. See `authentication/mine-authentication.yml`.
- Use the EU or US endpoint matching your account. See `lifecycle/mine-lifecycle.yml`.

## Steps
1. **List systems** — `GET /api/public-v1/system/List` to page through data sources by state (cursor pagination).
2. **Inspect one** — `GET /api/public-v1/system/{id}`.
3. **Add from the catalog** — `POST /api/public-v1/system/AddCatalogSystem` (`AddCatalogSystemPublicRequest`) for a known SaaS/system.
4. **Add a custom source** — `POST /api/public-v1/system/AddCustomSystem` (`AddCustomSystemPublicRequest`) for anything not in the catalog.
5. **Update properties** — `PATCH /api/public-v1/system/{id}` to edit inventory attributes.
6. **List business units** — `GET /api/public-v1/system/business-unit/list` to map systems to departments.
7. **AI autofill** — `POST /api/public-v1/system/{id}/ai-autofill` to trigger AI-suggested field values.

## Errors
- Error envelope `{ internalErrorCode, message }`. See `errors/mine-problem-types.yml`.

## Notes
- See `data-model/mine-data-model.yml` for how systems relate to business units, tickets, and assessments.
