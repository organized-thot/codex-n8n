# Community Nodes (npm) Security Policy

Installing community nodes from npm means installing unverified code into your n8n runtime.
Treat this as a supply-chain risk and validate before install.

Reference: n8n docs on risks and installation. (Read them.)
- Risks when using community nodes
- Install and manage community nodes

## Preferred order
1) Built-in n8n node
2) Verified community node (available from the nodes panel)
3) npm community node (only after validation)

## Validation checklist (minimum)
For any candidate package:
- Verify it is actually an n8n node package (n8n-nodes-* or scoped variant)
- Check npm signals:
  - publisher/maintainers are consistent
  - meaningful README + repo link
  - reasonable download counts / usage history
  - recent but not suspicious churn
- Check repo signals:
  - source code present
  - issues/PRs not dominated by malware reports
  - release tags match npm versions
- Inspect package contents (high-level):
  - does it include unexpected postinstall scripts?
  - does it embed obfuscated code?
  - does it reach unexpected network endpoints?
- Privilege minimization:
  - use least-privileged credentials in nodes
  - restrict outbound network where possible
- Deployment practice:
  - test-install in a disposable n8n instance first (recommended)
  - monitor logs and outbound traffic after installation

## Mandatory warnings to user
Always warn:
- npm community nodes are unverified code
- a supply chain attack has been reported in the n8n ecosystem; careful auditing is required