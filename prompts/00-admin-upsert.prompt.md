Create an n8n workflow named: "Admin Workflow Upsert"

Goal:
Provide a secure Tailnet-only endpoint that can create/update workflows via the n8n Public API.

Trigger:
Webhook: POST /admin/workflows/upsert

Security:
- Require header: X-Mobile-Secret
- Compare against secret stored in n8n variables/credentials (do NOT hardcode).
- On failure: respond HTTP 401 with { ok:false, error:"unauthorized" }.

Input payload:
{
  "name": "Workflow Name",
  "workflowJson": { ... },
  "active": false
}

Behavior:
1) Validate secret
2) Validate payload structure (name + workflowJson present)
3) Validate workflowJson:
   - must contain nodes + connections + settings
   - must be importable n8n workflow export JSON
4) Upsert logic:
   - Check if workflow exists by name via n8n API (v1)
   - If exists, update it
   - Else, create it
5) Optionally set active state (active=true/false)
6) Return:
{
  "ok": true,
  "action": "created" | "updated",
  "workflowId": "<id>",
  "editorUrl": "https://n8n.ermine-zebra.ts.net/workflow/<id>"
}

Important:
- Use HTTP Request nodes for n8n API calls.
- Auth to n8n API using header X-N8N-API-KEY (value from env/credentials).
- Provide: (1) FULL workflow JSON, (2) node-by-node explanation, (3) a curl test request, (4) expected response.
- Ensure the workflow itself is safe: do not echo secrets back.