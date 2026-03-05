# n8n-codex

A chat-first “workflow factory” for n8n Community. You use Codex (primarily inside the ChatGPT app) to:
- generate n8n workflow JSON from conversation
- validate + repair it before deployment
- deploy via an Admin Upsert endpoint
- trigger workflows from iOS Shortcuts with a JSON-only contract
- optionally discover and safely use npm community nodes (with security validation)

---

## Environment (current)

- n8n base URL (Tailnet-only via Tailscale Serve):
  https://n8n.ermine-zebra.ts.net

- API:
  /api/v1
- Auth header:
  X-N8N-API-KEY

- Security header required on all webhook workflows:
  X-Mobile-Secret: <secret>

The secret must be stored in n8n variables/credentials and never hardcoded in workflow JSON.

---

## Folder map

- AGENTS.md
  The operating contract for Codex. Defines required reads, security rules, output format.

- skills/
  Skills used by Codex for correct workflow JSON, expressions, node configuration, and validation.

- contracts/
  Stable “truth files” describing environment, webhook contract, deployment contract, and community-node security policy.

- prompts/
  Reusable prompts you paste into Codex (ChatGPT app) to generate workflows and deployment payloads.

- workflows/
  Workflow exports (.json). Store Admin Upsert and generated workflows here for history/versioning.

- deploy/examples/
  Curl examples and test payloads.

---

## Quick start (recommended)

### Step 1: Bootstrap Admin Upsert (one-time manual import)
1) Run prompt: prompts/00-admin-upsert.prompt.md
2) Save JSON to: workflows/admin-upsert.json
3) Import into n8n UI (Settings → Import workflow or via the canvas import)
4) Test deployment endpoint:
   deploy/examples/deploy-admin-upsert.curl.txt

### Step 2: Generate + deploy a workflow from chat
1) Run prompt: prompts/10-workflow-from-chat.prompt.md
2) Codex returns:
   - workflow JSON
   - validation checklist and corrections (repair loop)
   - deploy payload for Admin Upsert
   - test harness payload + expected response
3) Deploy by POSTing to:
   https://n8n.ermine-zebra.ts.net/webhook/admin/workflows/upsert

### Step 3: Trigger from iOS Shortcuts
Create a Shortcut:
- Action: “Get Contents of URL”
- Method: POST
- URL: https://n8n.ermine-zebra.ts.net/webhook/<your-webhook-path>
- Headers:
  - Content-Type: application/json
  - X-Mobile-Secret: <secret>
- Body: JSON (dictionary) following contracts/mobile-webhook-contract.md

---

## Community nodes (npm) — safe usage workflow

Community nodes can execute arbitrary code in your n8n runtime. Treat them like installing a random npm package into a production automation server.

Use prompt:
- prompts/40-community-node-intake.prompt.md

It will:
- find candidate node packages
- prefer verified community nodes when available
- run a security validation checklist (publisher, repo, downloads, code signals)
- recommend a test-first installation approach
- output the exact n8n UI install steps (or manual approach) and required env vars

Read:
- contracts/community-nodes-security.md

---

## Troubleshooting

### “Webhook URL / redirects are wrong”
Confirm n8n env vars:
- N8N_HOST=n8n.ermine-zebra.ts.net
- N8N_EDITOR_BASE_URL=https://n8n.ermine-zebra.ts.net
- WEBHOOK_URL=https://n8n.ermine-zebra.ts.net

### “Workflow won’t import”
Use:
- prompts/90-debug-repair.prompt.md
Provide the JSON and n8n error message. Codex will return corrected JSON + deploy payload.

### “Community node works in test but not when active / as tool”
Ensure:
- N8N_COMMUNITY_PACKAGES_ALLOW_TOOL_USAGE=true (for tool usage)
and restart the container.

---

## How Codex should be used (best practice)
- Keep AGENTS.md + contracts stable.
- Generate workflows with prompts/10-workflow-from-chat.prompt.md.
- Always deploy through Admin Upsert so you keep a consistent pipeline and logs.
- Always use the validation+repair loop and test harness before relying on a workflow.