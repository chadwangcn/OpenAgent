# TestRunReceipt v1

Each test execution returns a sanitized receipt with this minimum structure:

```yaml
schema_version: lumi.test-run-receipt.v1
paperclip_task_id: <task-id>
test_type: app | api
agent:
  agent_id: <agent-id>
  version: <agent-version>
skills:
  - name: <skill>
    version_or_commit: <pin>
tool:
  repository: <repo>
  commit_or_image_digest: <pin>
case_set:
  repository: <repo>
  commit: <full-commit>
  case_ids: []
subject:
  source_commit: <optional>
  artifact_or_deployed_digest: <pin>
environment_ref: <logical-name>
started_at: <UTC>
finished_at: <UTC>
summary:
  total: 0
  passed: 0
  failed: 0
  blocked: 0
case_results:
  - case_id: <id>
    status: passed | failed | blocked | skipped
    assertion_summary: <sanitized>
    evidence_refs: []
findings:
  - finding_id: <id>
    classification: product | case | tool | environment | spec_ambiguity
    next_owner: <one-owner>
evidence_index:
  - kind: <type>
    artifact_ref: <non-secret-ref>
    sha256: <64-hex>
cleanup_status: passed | failed | not_required
disposition: passed | failed | blocked
```

Never include raw tokens, passwords, device secrets, authorization headers, Pod/ADB endpoints, private user data or expiring signed URLs. Paperclip comments should carry this receipt or a compact summary plus a durable receipt artifact reference.
