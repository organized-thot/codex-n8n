# Community nodes

Use this file when a task asks for a community node or npm package.
Built-in and verified nodes stay the default choice because npm nodes
are unverified code in the n8n runtime.

## Decision order

Use this order of preference:
1. Built-in n8n node
2. Verified community node
3. npm community node after validation

## Required validation

For any npm package candidate:
- Verify it is an n8n node package.
- Check npm publisher, maintainers, repo link, release history, and
  usage signals.
- Inspect the repo for real source code and suspicious security
  reports.
- Inspect package contents for `postinstall` scripts, obfuscated code,
  or unexpected network behavior.
- Use least-privileged credentials.
- Recommend test-first installation in a disposable instance.

## Mandatory warning

Always tell the user:
- npm community nodes are unverified code
- the n8n ecosystem has had supply-chain risk
- installation needs explicit validation before production use

## Delivery requirements

After validation, provide:
- the risk callout
- install steps for the n8n UI or manual install path
- configuration guidance
