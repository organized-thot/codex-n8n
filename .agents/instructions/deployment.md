# Deployment

This repo deploys workflows through a chat-first control plane, but the
approved direction is a hybrid model. Use `Admin Upsert` for normal
workflow updates and reserve a bootstrap or recovery script for cases
where the control plane itself must be repaired.

## Current endpoint

The current deploy endpoint is
`POST https://n8n.ermine-zebra.ts.net/webhook/admin/workflows/upsert`.

Send these headers:
- `Content-Type: application/json`
- `X-Mobile-Secret: <secret>`

The current contract documents this payload shape:

```json
{
  "name": "Workflow Name",
  "workflowJson": {},
  "active": false,
  "tags": ["optional", "metadata"]
}
```

Verify live behavior before depending on fields beyond `name` and
`workflowJson`.

## Approved direction

- Support `workflowId`-driven updates when the control plane is
  revised.
- Keep activate and deactivate as separate API operations.
- Do not rely on workflow name matching for long-term idempotency.
- Use a bootstrap or recovery PowerShell path when `Admin Upsert` is
  missing or broken.

## Deployment guardrails

- Verify the final workflow state after deploy.
- Treat duplicate workflow names as an ambiguity that must be resolved,
  not as a safe match.
- Keep `TEST_REPORT.md` up to date for resumed end-to-end test runs.
- If the live instance contradicts the contract, update the contract
  before claiming success.
