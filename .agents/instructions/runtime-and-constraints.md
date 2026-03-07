# Runtime and constraints

This file records the approved runtime assumptions for this repo. Use
it when older contracts or prompt packs do not match proven n8n
Community behavior.

## Source of truth

Use this precedence order when instructions conflict:
1. Validated runtime behavior from live probing
2. Approved handoffs in `.agents/handoffs/`
3. `AGENTS.md` and `.agents/instructions/`
4. `contracts/` and prompt packs

## Current runtime facts

- Base URL: `https://n8n.ermine-zebra.ts.net`
- Tailscale Serve maps the Tailnet URL to `http://127.0.0.1:5678`.
- The REST API lives under `/api/v1` and uses `X-N8N-API-KEY`.
- The runtime is n8n Community in Docker Desktop with WSL2-friendly
  paths.
- The current compose project is `compose-n8n`.
- The containers are `compose-n8n-ts` and `compose-n8n-n8n`.
- Secrets come from credentials or environment-backed bootstrap logic,
  not n8n Variables.

## Constraint breakpoint rule

When you prove a requirement cannot be satisfied by this runtime:
1. Stop the failing path.
2. Record the exact constraint and the evidence.
3. Propose the corrected contract, workflow shape, or deploy flow.
4. Resume only after the corrected assumption is explicit.

## Current overrides

- Use native n8n credential-backed webhook auth instead of custom
  secret logic when the platform supports it.
- Expect native unauthorized behavior from n8n auth. Do not require a
  literal `401` unless the design actually controls it.
- Keep JSON intake and file upload intake as separate workflows.
- Treat workflow activation and deactivation as separate operations
  from workflow create or update.
- Prefer explicit workflow IDs over name matching because duplicate
  live workflow names have already existed.
