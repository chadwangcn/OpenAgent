# Prismloop APP Run Contract

## Task input

```yaml
figma:
  url: <exact-url>
  version: <exact-version>
  node_ids: [<node-id>]
case_set:
  repository: chadwangcn/Prismloop
  commit: <full-commit>
  index: cases/index.json
  case_ids: [APP-...]
subject:
  apk_artifact_ref: <immutable-ref>
  apk_sha256: <64-hex>
  android_package: <package>
environment_ref: <logical-environment>
```

## Service sequence

1. `GET $PRISMLOOP_BASE_URL/healthz`
2. `GET $PRISMLOOP_BASE_URL/v1/media-capabilities?environment_ref=...`
3. `POST $PRISMLOOP_BASE_URL/v1/media-runs`
4. `GET $PRISMLOOP_BASE_URL/v1/media-runs/{run_id}` until terminal within the bounded observation window
5. `POST $PRISMLOOP_BASE_URL/v1/media-runs/{run_id}:cancel` only when the Task explicitly authorizes cancellation

Terminal tool states are `completed`, `capability_unavailable`, `error`, and `canceled`. `queued` and `running` are not test conclusions.

Use only actions declared by the current request schema, including UI launch/tap/swipe/text/key/dump, media input, waits, screenshots and supported capture actions. A Case requiring an unverified capability must be blocked or partially executed; it must not be silently skipped.

## Evidence interpretation

- `outputs[]`: raw evidence artifacts such as screen images, video, audio, UI tree or execution log.
- `stream_receipts[]`: continuity and timing evidence; zero restarts/discontinuities are required only when the Case states that invariant.
- `input_snapshot`: proof of the exact input used for replay or A/B comparison.
- `evidence_index`: authoritative list of evidence references and hashes.
- `error`: tool failure evidence, not automatically a product defect.

The APP verdict must map every Case assertion to one or more evidence items. Visual judgment must retain Figma version/node identity and should use structured diff data when available, with manual review explicitly labelled when it is used.
