---
generated: '2026-07-20'
method: generated
name: Run an assessment and trigger third-party risk (TPRM)
description: List templates, create an assessment from a template, submit its form, and trigger a TPRM event in MineOS.
api: openapi/mine-openapi-original.json
operations:
  - GET /api/public-v1/template/List
  - POST /api/public-v1/assessment/from-template
  - POST /api/public-v1/assessment/form-submission
  - GET /api/public-v1/assessment/List
  - POST /api/public-v1/tprm/trigger
source: >-
  Grounded in openapi/mine-openapi-original.json assessment/tprm paths (verified
  verbatim; spec declares no operationIds, so steps cite METHOD + path).
---

# Run an assessment and trigger third-party risk (TPRM)

Use this to stand up an assessment (e.g. a vendor / privacy questionnaire) and drive a third-party risk workflow.

## Auth
- API-key Bearer: `Authorization: Bearer <APIKey>` over HTTPS. See `authentication/mine-authentication.yml`.
- Use the EU or US endpoint matching your account.

## Steps
1. **List templates** — `GET /api/public-v1/template/List` to find an assessment template for the company.
2. **Create from template** — `POST /api/public-v1/assessment/from-template` (`CreateFromTemplateRequest`). Capture the new assessment id.
3. **List / inspect assessments** — `GET /api/public-v1/assessment/List` (by type + pagination); `GET /api/public-v1/assessment/{id}` for detail.
4. **Invite collaborators** — `POST /api/public-v1/assessment/{id}/collaborators` (`CollaboratorInviteRequest`).
5. **Submit the form** — `POST /api/public-v1/assessment/form-submission`; attach files with `POST /api/public-v1/assessment/form-submission/{id}/attachment` (triggers RAG indexing). Read back with `GET /api/public-v1/assessment/{id}/form-submission`.
6. **Trigger TPRM** — `POST /api/public-v1/tprm/trigger` to fire a Third-Party Risk Management event.

## Errors
- Error envelope `{ internalErrorCode, message }`. See `errors/mine-problem-types.yml`.

## Notes
- Pagination is cursor-based. See `conventions/mine-conventions.yml`.
