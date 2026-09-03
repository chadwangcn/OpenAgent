---
name: lumi-ai-native-delivery
description: Govern Lumi delivery as an evidence-driven AI-native SDLC loop. Use when planning, dispatching, implementing, testing, reviewing, releasing, deploying, accepting, or improving a Paperclip task so each stage has exact artifacts, one owner, explicit gates, and auditable feedback.
---

# Lumi AI-native delivery

Use `workflows/lumi-ai-native-sdlc.yaml` in the OpenAgent repository as the organization workflow. Apply the narrower repository `AGENTS.md`, task package, D0 contract, Figma pin, tool Skill, and Case rules at the same time; this Skill does not override their scope or authority.

## Start from a bounded delivery record

Before acting, identify:

- `delivery_class`, business outcome, in-scope and out-of-scope work;
- target repository or system, exact contract/design/Case pins and environment;
- `delivery_key` used to query existing Paperclip work before creating or reassigning anything;
- current gate, required evidence, one Owner, one `next_owner`, and the named terminal acceptor.

If any field needed for the current gate is missing, emit a `BlockerNotice`; do not guess, use a floating branch, or create a parallel task.

## Move by artifacts, not claims

Use this chain when the selected `delivery_class` requires the stage:

1. `IntentRecord`: outcome, users/systems, constraints, exclusions and success measure.
2. `ContractOrDesignRecord` plus executable acceptance criteria.
3. `WorkPackage` and `DispatchReceipt`: dependency DAG, exact pins, verification and bounded Owner.
4. `DeliveryNotice`: source commit/tree plus literal self-test output from the implementation Owner.
5. Independent `ReviewReceipt` or `TestRunReceipt` against an immutable subject and pinned Case set.
6. `PRRef`, main readback, successful CI run and full OCI digest.
7. Explicitly authorized SRE deployment of that digest and a `DeploymentReceipt` with runtime readback.
8. External I/O or business acceptance by the named independent acceptor.
9. `ImprovementCandidate` for repeated defects, latency, drift or capability gaps.

An implementation Owner must verify its own work, but its evidence only advances the task to `in_review`. The same Owner cannot supply the independent approval that makes its work terminal.

## Keep Paperclip state honest

- `backlog`: a dependency, environment capability or authority is missing. Attach the exact blocker and next action.
- `todo`: every prerequisite is present and the named Owner can execute now.
- `in_progress`: an active run is working the stated gate.
- `in_review`: Owner evidence exists, but an independent review, test, release, deployment or acceptance gate remains.
- `done`: only after the terminal gate for `delivery_class` has a named, readable receipt.
- `cancelled`: only for explicit withdrawal, deduplication or supersession, with the replacement reference.

Do not treat a queued-run cancellation caused by reassignment as a product failure. Preserve the run record, identify the current Owner, and wake only when the task is actually ready.

## Diagnose and route failures

Every failure or block must include:

- `blocker_code` and affected gate;
- evidence reference or safe command-result summary;
- exactly one `next_owner` and one `required_action`;
- whether human authorization is required and the smallest decision requested.

Do not route a task back to its source merely because that source requested coordination. Do not let PM, reviewer, or architect become the implementation Owner unless the task explicitly assigns that role.

## Close the learning loop

When a failure pattern, repeated manual step, excessive run time, or instruction drift is observed, create an `ImprovementCandidate` and classify it into exactly one primary lane:

- Agent definition;
- Skill or Workflow;
- Tool;
- Case;
- Product/component;
- Environment.

Record frequency, elapsed-time impact, error rate, evidence sample, suspected root cause, proposed experiment and acceptance metric. Keep the original delivery task scoped; improve the selected lane through its own reviewed change. Add representative incidents to the Agent eval or Case suite so the correction is regression-tested.

Never include secret values, device credentials, private signed URLs, raw user content, or unrestricted logs in Paperclip, Git, prompts or receipts.
