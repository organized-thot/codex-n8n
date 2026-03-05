# Environment

Base URL:
https://n8n.ermine-zebra.ts.net

Tailscale Serve:
https://n8n.ermine-zebra.ts.net → http://127.0.0.1:5678 (Tailnet-only)

API:
- Base path: /api/v1
- Auth header: X-N8N-API-KEY

Docker:
- compose project: compose-n8n
- containers:
  - compose-n8n-ts (tailscale sidecar)
  - compose-n8n-n8n (n8n)

Community nodes env vars (if needed):
- N8N_COMMUNITY_PACKAGES_ENABLED=true
- N8N_VERIFIED_PACKAGES_ENABLED=true (controls verified node visibility in UI)
- N8N_COMMUNITY_PACKAGES_ALLOW_TOOL_USAGE=true (required for community nodes as AI tools)