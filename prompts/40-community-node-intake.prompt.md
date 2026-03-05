Help me choose and safely use an n8n community node from npm.

Goal:
Find candidate nodes and perform security validation before recommending installation.

Input:
- Desired capability: <describe what node should do>
- Constraints: self-hosted n8n Community, Tailnet-only, Docker

Process:
1) Prefer built-in nodes or verified community nodes first.
2) If npm community nodes are needed:
   - identify 2–5 candidate packages on npm
   - for each:
     - summarize what it does
     - list publisher/maintainer signals
     - repo link and activity signals
     - download/adoption signals
     - dependency and install-script red flags
     - risk rating (low/med/high) with justification
   - explicitly reference n8n documentation about risks and install methods.
3) Provide installation instructions for self-hosted n8n:
   - via n8n GUI (Settings → Community nodes) where available
   - or manual method if GUI isn’t possible
4) If the node is intended to be used as an AI Agent tool:
   - mention the env var N8N_COMMUNITY_PACKAGES_ALLOW_TOOL_USAGE=true
5) Provide a “test-first plan”:
   - install in a disposable instance first (recommended)
   - then verify node appears and works
   - then monitor logs/outbound calls

Output:
- Recommended package (or “don’t use one”)
- Validation checklist results
- Step-by-step install + verification