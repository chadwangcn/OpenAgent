---
name: nightwatch-api-testing
description: Use NightWatch to execute version-pinned Lumi API black-box cases, enforce environment policy and secret-by-reference, collect sanitized evidence, and classify findings. Use for API, event, WebSocket, or SDK-visible contract validation, not for modifying backend code or publishing formal D0 contracts.
---

# NightWatch API Testing

Use NightWatch as the API registry, planning, policy, execution, evidence and Finding engine. D0 remains the formal API definition source, and the Agent remains responsible for the final Case verdict.

## Required sources

Resolve inputs in this order:

1. Paperclip Task: D0 definition commit/path/digest, Case repository/commit/IDs, deployed subject digest and DeploymentReceipt.
2. Paperclip Agent environment: NightWatch endpoint, named environment and the canonical `LUMI_API_BASE_URL`; credentials are Secret References.
3. NightWatch repository: only published schemas, Case index and tool interface; do not read local credential files.

Read [references/environment-contract.md](references/environment-contract.md) when preparing credentials or an environment. Read [references/run-contract.md](references/run-contract.md) before importing a contract, starting a run, or interpreting evidence.

## Execution rules

1. Verify the D0 commit/path/digest and Case commit. Never infer a formal contract from a component implementation or floating `main`.
2. Verify the DeploymentReceipt and deployed subject digest. Source, OCI candidate and deployed runtime are distinct facts.
3. Select the named NightWatch environment and apply its policy gate before resolving credentials or sending traffic.
4. Use `LUMI_API_BASE_URL` as the only Lumi endpoint value. Tool-specific aliases must be created inside the NightWatch adapter, not maintained as competing Paperclip values.
5. Lease only credential names required by the selected Case/auth profile. Never pass the whole parent environment to an executor.
6. Generate or load a TestPlan that maps every selected Case to the pinned contract and an allowed environment.
7. Start the run with an idempotency key and bounded request/duration/parallelism budgets. Do not run destructive, fuzz or load cases without explicit environment permission.
8. Treat process success, HTTP 200 and health responses as transport evidence only. Evaluate each Case assertion and failure semantic.
9. Store sanitized request/response evidence, reports and logs in the Artifact Store. Paperclip receives a receipt summary, Finding IDs, artifact references and hashes.
10. Reproduce failures within the Task budget, then classify them as `product`, `case`, `tool`, `environment`, or `spec_ambiguity` with one next owner.

## Stop conditions

Stop with a `BlockerNotice` on contract digest mismatch, missing deployment evidence, missing Secret binding, denied environment policy, evidence integrity failure, or unapproved destructive scope.

Return a `TestRunReceipt` following `$lumi-test-case-governance`. Do not modify the tested service, D0 definitions, routing or deployment, and do not publish a GitHub defect automatically unless the Task explicitly authorizes that mutation.
