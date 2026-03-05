# Codex Agent Instructions (n8n-codex)

You are operating inside the `n8n-codex` repository.

Your mission:
1) Generate correct, importable n8n workflow JSON
2) Validate + repair before deployment (never “ship” broken JSON)
3) Provide a test harness payload and expected results for each workflow
4) Deploy via Admin Upsert endpoint instructions
5) When asked to use community nodes (npm), perform security validation first and prefer verified nodes.

---

## Required reads (always do this first)
1) contracts/environment.md
2) contracts/mobile-webhook-contract.md
3) contracts/deployment-contract.md
4) contracts/community-nodes-security.md

When generating a workflow, also read:
- prompts/10-workflow-from-chat.prompt.md

---

## Skills available
Skills live in `skills/`. Use them actively, not passively.

Preferred usage order:
1. n8n-mcp-tools-expert (search + authoritative node/config references)
2. n8n-node-configuration (correct node settings + operation patterns)
3. n8n-expression-syntax (expressions, common mistakes)
4. n8n-workflow-patterns (common architectures for webhook/API/scheduled flows)
5. n8n-validation-expert (validate JSON + catch schema/config errors)
6. n8n-code-javascript (Code node patterns + error handling)
7. n8n-code-python (if Python is required)

---

## Universal workflow requirements
All generated workflows MUST:
- Be valid n8n JSON and importable
- Avoid deprecated nodes
- Include clear node names
- Include a Webhook Response node for webhook flows
- Include error handling where reasonable
- Include a security gate for webhooks:
  - require header `X-Mobile-Secret`
  - compare to a secret stored in n8n variables/credentials
  - fail closed (401) when invalid

Do NOT hardcode secrets in JSON.

---

## Validation + repair loop (mandatory)
Before final output:
1) Run a validation pass (use n8n-validation-expert + expression-syntax skill)
2) Identify common failure points:
   - missing/incorrect `connections`
   - invalid expressions
   - missing Webhook Response node
   - node type/version mismatches
3) If any issue is detected:
   - produce a corrected JSON
   - explain what was fixed

Always output “FINAL JSON” only after validation.

---

## Self-testing harness (mandatory)
For every webhook workflow output:
- Provide:
  - curl command example (using placeholders)
  - minimal JSON payload example
  - required headers
  - expected HTTP status + expected JSON shape
- If the workflow calls third-party APIs, provide a “dry-run test mode” option using mock data.

---

## Deployment model
Workflows are deployed via Admin Upsert workflow:

POST https://n8n.ermine-zebra.ts.net/webhook/admin/workflows/upsert

Headers:
- Content-Type: application/json
- X-Mobile-Secret: <secret>

Payload:
{
  "name": "Workflow Name",
  "workflowJson": { ... }
}

The Admin Upsert workflow calls the n8n API (v1) using X-N8N-API-KEY.

---

## Community nodes (npm) policy
When asked to use a community node:
1) Prefer official nodes and verified community nodes when possible.
2) If using npm packages:
   - run the security checklist in contracts/community-nodes-security.md
   - warn about supply chain risks
   - recommend test-first installation in a disposable instance if possible
3) Only after validation:
   - propose the node
   - provide install steps (GUI or manual, per n8n docs)
   - provide configuration guidance

Never recommend installing a community node without a risk callout and validation steps.