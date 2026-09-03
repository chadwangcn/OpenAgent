# Prismloop Agent Environment Contract

## Plain environment variables

| Variable | Required | Source | Meaning |
| --- | --- | --- | --- |
| `PRISMLOOP_BASE_URL` | yes | Paperclip Agent environment | Prismloop internal service base URL; no trailing API path |
| `PRISMLOOP_ENVIRONMENT_REF` | yes | Paperclip Agent environment | Default logical cloud/real-device environment |
| `PRISMLOOP_ARTIFACT_STORE_REF` | yes | Paperclip Agent environment | Non-secret logical store reference used in requests |
| `TEST_EVIDENCE_ROOT` | optional | Paperclip Agent environment | Local transient evidence root; must not be committed |

## Secret bindings

| Variable | When required | Source |
| --- | --- | --- |
| `FIGMA_ACCESS_TOKEN` | when Figma content cannot be resolved through an authenticated connector | Paperclip Secret Reference |
| `GITHUB_TOKEN` | when reading private Case/APK metadata or writing an approved Case PR | Paperclip Secret Reference |

Prismloop service-side cloud-phone, TOS, STS, Pod and ADB credentials are not Agent variables. The service owns them and exposes only `environment_ref` and `artifact_ref`.

Do not read `config/env.local.json`, shell history, another Agent's environment, or a developer Keychain as fallback. Report only missing variable names; never print values.

Task-specific Figma URLs, node IDs, APK references, Case IDs and subject digests are Task inputs, not global environment variables.
