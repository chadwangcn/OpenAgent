# Lumi Test Case Lifecycle

## Required fields

Every Case needs:

- stable `case_id`, title, owner, status and priority;
- immutable `design_ref` or `contract_ref`;
- applicability and supported environments;
- preconditions and named credential references;
- deterministic inputs and ordered steps;
- assertions with expected and observable values;
- cleanup/teardown and resource-leak expectation;
- required evidence types;
- supersession/deprecation link when meaning changes.

## Lifecycle

```text
draft -> review -> approved -> active -> deprecated -> retired
                     |            |
                     +-> revised <-+
```

Only approved/active Cases count toward a release gate. A draft may be executed for exploration but its result cannot reject a release.

## Execution feedback

Execution results do not automatically change a Case. Open a Case-maintenance change only when evidence demonstrates a requirement change, coverage gap or Case defect. Preserve the original run, evidence and Case commit so the correction is auditable.

For retest, use the same Case commit when validating a product fix. If the Case itself changes, record both old and new Case commits and explain why the previous result is not directly comparable.
