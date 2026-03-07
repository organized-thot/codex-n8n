# Workflow authoring

Use this guidance when creating or revising n8n workflows for this
repo. The goal is importable JSON, validated before handoff, with a
runnable test harness.

## Preferred skills

Load and use skills in this order when they apply:
1. `n8n-mcp-tools-expert`
2. `n8n-node-configuration`
3. `n8n-expression-syntax`
4. `n8n-workflow-patterns`
5. `n8n-validation-expert`
6. `n8n-code-javascript`
7. `n8n-code-python`

## Universal workflow requirements

- Produce valid, importable n8n JSON.
- Avoid deprecated nodes.
- Use clear node names.
- Add a `Webhook Response` node for webhook flows.
- Add error handling when the workflow can fail in predictable ways.
- Never hardcode secrets in workflow JSON.
- For webhook auth, prefer runtime-managed credentials or
  environment-backed bootstrap over inline secret comparisons.
- When documenting auth failures, describe the expected unauthorized
  outcome instead of assuming a literal `401`.

## Validation and repair loop

Before final output:
1. Run a validation pass with the validation and expression guidance.
2. Check for missing or incorrect `connections`.
3. Check for invalid expressions.
4. Check for missing `Webhook Response` nodes on webhook flows.
5. Check for node type or version mismatches.
6. If any issue appears, correct the JSON and explain what changed.

Only label output as `FINAL JSON` after validation passes.

## Test harness requirements

For every webhook workflow, provide:
- a `curl` example with placeholders
- the required headers
- a minimal JSON payload
- the expected HTTP status
- the expected JSON response shape

If the workflow calls third-party APIs, also provide a dry-run or
mock-data path for safe testing.
