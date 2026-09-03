---
name: lumi-test-case-governance
description: Design, review, version, and evolve Lumi APP or API test cases while preserving traceability to Figma or D0 contracts, separating Case defects from product/tool/environment failures, and producing reproducible test receipts. Use for Case maintenance and test-result governance, not for implementing product or test-tool code.
---

# Lumi Test Case Governance

Treat test Cases as durable product assets. A Case describes externally visible behavior and evidence; it must not encode tool internals, live credentials, mutable URLs or private implementation details.

Read [references/case-lifecycle.md](references/case-lifecycle.md) when adding, changing, deprecating or reviewing Cases. Read [references/test-run-receipt.md](references/test-run-receipt.md) when executing tests or reporting results.

## Source rules

- APP Case intent binds an exact Figma file/version/node and, when relevant, a product requirement or D0 Case.
- API Case intent binds an exact D0 repository commit/path/digest. Component code is not the formal contract source.
- Every execution pins the Case repository commit and Case IDs. Never report against floating `main` or `latest`.
- Case fixtures contain synthetic or reference-based data only. Secrets are named references resolved at run time.

## Change classification

Before editing a Case, classify the reason:

- `requirement_change`: approved design or formal contract changed.
- `coverage_gap`: behavior was valid but untested.
- `case_defect`: assertion, data, sequence or cleanup was wrong.
- `tool_capability_gap`: the Case is valid but the executor cannot perform or observe it.
- `product_defect`: the implementation violates an unchanged Case.
- `environment_failure`: credentials, network, device or deployment prevented observation.

Only the first three authorize a Case change. Tool, product and environment findings must be routed without weakening the Case to make a run pass.

## Review gates

A Case change must include an immutable source reference, stable ID, priority, preconditions, inputs, steps, assertions, cleanup, evidence requirements and applicability. Review negative and boundary behavior as well as the happy path. Retain history when IDs are superseded; do not silently reuse an ID with different business meaning.

Case PRs must not modify test-tool implementation. Tool PRs must not silently rewrite Case expectations. A bootstrap migration may touch both only when the scope explicitly says so and preserves a mapping from old IDs/paths to new ones.

Use a machine-readable index as the only discovery entrypoint. Raw execution output is never a Case asset.
