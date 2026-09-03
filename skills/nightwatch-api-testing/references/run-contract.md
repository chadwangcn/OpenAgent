# NightWatch API Run Contract

## Task input

```yaml
api_definition:
  repository: chadwangcn/Lumi-Agent-Mind
  commit: <full-commit>
  paths: [definitions/...]
  sha256: <digest>
case_set:
  repository: chadwangcn/NightWatch
  commit: <full-commit>
  index: cases/index.json
  case_ids: [API-...]
subject:
  deployed_digest: <oci-or-release-digest>
  deployment_receipt_ref: <receipt-ref>
environment: <named-environment>
```

## Tool sequence

1. Resolve and validate the API registry entry from the pinned D0 definition.
2. Resolve selected Case IDs through `cases/index.json` and validate them against `nightwatch/schemas/test_case/v1.json` or their declared adapter schema.
3. Create a TestPlan with budgets, environment, auth profile and exact Case IDs.
4. Run the NightWatch policy gate before credential materialization.
5. Start the execution through the deployed NightWatch control API. Use legacy Newman collection endpoints only when the Case index declares a Postman adapter.
6. Read terminal `execution_result`, evidence bundle and Findings; do not infer completion from an HTTP request returning successfully.

During the transition period, a Postman-backed Case may invoke `/api/run`, `/api/run-batch` or the repository's `npm run newman:*` entrypoint. The resulting report must still be normalized into the shared receipt and evidence model.

## Result interpretation

- Per-Case result is authoritative for pass/fail.
- Cleanup failure prevents a clean pass when the Case requires resource restoration.
- Transport, credential and network failures are `environment` until evidence identifies a product behavior.
- Contract ambiguity is reported to the architecture owner; the API test Agent does not edit D0 definitions.
- Finding publication is separate from Finding creation and requires explicit Task authority plus deduplication.

Evidence bundles must redact authorization headers, tokens, passwords, device secrets, personal data and private URLs before persistence.
