---
name: prismloop-app-testing
description: Use Prismloop to execute version-pinned Android APP test cases on real or cloud devices, including UI actions, media injection, screenshot evidence, bounded monitoring, and failure classification. Use for APP test execution or Prismloop capability diagnosis, not for modifying APP code or authoring product requirements.
---

# Prismloop APP Testing

Use Prismloop as an execution and evidence service. The Agent, not Prismloop, interprets Figma, selects Case assertions, and decides pass/fail.

## Required sources

Resolve inputs in this order:

1. Paperclip Task: exact Figma URL/version/node IDs, Case repository/commit/IDs, APK artifact reference/SHA-256/package, and requested environment.
2. Paperclip Agent environment: Prismloop endpoint, default environment and artifact store; Secrets are injected by reference.
3. Prismloop repository: only its published schemas and usage documents, never a local secret file or a floating project default.

Read [references/environment-contract.md](references/environment-contract.md) when preparing the runtime or diagnosing configuration. Read [references/run-contract.md](references/run-contract.md) before executing a Case or interpreting evidence.

## Execution rules

1. Reject a Task that lacks an exact Figma version, Case commit, APK SHA-256 or package name. Do not replace them with `latest`.
2. Verify the APK digest before device installation. A reachable download URL is not artifact identity.
3. Call `/healthz`, then `/v1/media-capabilities` for every required capability. Do not bypass `capability_unavailable`.
4. Translate Case steps into a Prismloop `MediaRunRequest`; keep credentials, Pod IDs, ADB endpoints and signed URLs out of the request.
5. Submit with an idempotency key derived from Task ID, Case ID, subject digest and attempt number.
6. Monitor only for a bounded window. If the run remains non-terminal, persist `run_id` and the next check condition, then end the heartbeat instead of polling indefinitely.
7. Treat Prismloop `completed` as “tool sequence completed”, not “Case passed”. Evaluate every Case assertion against the Figma reference and returned evidence.
8. Store raw screenshot, recording, UI tree and logs in the configured Artifact Store. Paperclip receives only sanitized summaries, `artifact_ref` and SHA-256.
9. Classify each failure as `product`, `case`, `tool`, `environment`, or `spec_ambiguity`, and assign one next owner.
10. On retest, preserve the Case commit unless an approved Case correction exists; always use a new subject digest or attempt key.

## Stop conditions

Stop with a `BlockerNotice` when required input or Secret binding is missing, the APK digest mismatches, a required capability is unavailable, evidence integrity fails, or the requested device/environment exceeds the Task authority.

Return a `TestRunReceipt` following the shared `$lumi-test-case-governance` format. Never modify APP code, deploy an APK to production, or turn an observed failure into a tool change without a separate `test_tool_improvement` task.
