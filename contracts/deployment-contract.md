# Deployment Contract (Admin Upsert)

Admin Upsert endpoint:
POST https://n8n.ermine-zebra.ts.net/webhook/admin/workflows/upsert

Headers:
- Content-Type: application/json
- X-Mobile-Secret: <secret>

Payload:
{
  "name": "Workflow Name",
  "workflowJson": { ... },
  "active": false,
  "tags": ["optional", "metadata"]
}

Behavior:
- Validate secret header
- Validate that workflowJson is valid n8n workflow export JSON
- Create or update the workflow using n8n API (/api/v1)
- Return:
  { ok, workflowId, editorUrl, action: "created"|"updated" }