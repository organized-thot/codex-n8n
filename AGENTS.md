# n8n-codex

`n8n-codex` is a Codex-first workflow factory for n8n Community
running on Windows + Docker Desktop behind a Tailnet-only endpoint.

## Read first

Before workflow or deployment work, read:
1. `contracts/environment.md`
2. `contracts/mobile-webhook-contract.md`
3. `contracts/deployment-contract.md`
4. `contracts/community-nodes-security.md`

When generating a workflow, also read
`prompts/10-workflow-from-chat.prompt.md`.

## Core rules

- Treat validated runtime behavior and approved handoffs as higher
  priority than stale repo docs.
- Stop when a contract is proven incompatible with the runtime.
  Document the mismatch, propose the corrected contract, and avoid
  debugging the impossible path.
- Never hardcode secrets in workflow JSON.
- Do not assume n8n Variables are available in this instance.
- Use the linked instruction files for task-specific guidance.

## Detailed instructions

- [Runtime and constraints](.agents/instructions/runtime-and-constraints.md)
- [Workflow authoring](.agents/instructions/workflow-authoring.md)
- [Deployment](.agents/instructions/deployment.md)
- [Community nodes](.agents/instructions/community-nodes.md)
