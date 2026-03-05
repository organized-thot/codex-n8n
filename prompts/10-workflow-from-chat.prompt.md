You are generating an n8n workflow for the environment described in:
- AGENTS.md
- contracts/environment.md
- contracts/mobile-webhook-contract.md

User request:
<PASTE REQUEST OR SUMMARIZE CONVERSATION INTO A CLEAR SPEC>

Requirements:
- Must validate X-Mobile-Secret for any webhook trigger.
- JSON-only request bodies (no multipart) for mobile triggers.
- Must be compatible with n8n Community.
- Must include a Webhook Response node returning a stable JSON response.

Mandatory upgrades:
A) Validation + repair loop:
- Perform a validation pass using the available n8n skills.
- Identify likely import/runtime failures.
- Output corrected JSON if needed.

B) Self-testing harness:
- Provide:
  1) curl example to trigger the workflow
  2) minimal JSON payload example
  3) expected HTTP status + response JSON shape
  4) “dry-run mode” guidance if external APIs are involved

Deployment:
- Provide an Admin Upsert payload:
  POST https://n8n.ermine-zebra.ts.net/webhook/admin/workflows/upsert
  Headers: Content-Type: application/json, X-Mobile-Secret: <secret>
  Body: { name, workflowJson, active:false }

Output format (exact):
1) FINAL WORKFLOW JSON (only one JSON object, no commentary inside)
2) VALIDATION REPORT (bullet list)
3) DEPLOY REQUEST (curl snippet + body JSON)
4) TEST HARNESS (curl + payload + expected response)
5) NOTES (optional)