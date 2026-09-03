# NightWatch Agent Environment Contract

## Plain environment variables

| Variable | Required | Source | Meaning |
| --- | --- | --- | --- |
| `NIGHTWATCH_BASE_URL` | yes | Paperclip Agent environment | NightWatch service/control endpoint |
| `NIGHTWATCH_ENVIRONMENT` | yes | Paperclip Agent environment | Named policy environment such as `lumi-staging` |
| `LUMI_API_BASE_URL` | yes | Paperclip Agent environment | Canonical target Lumi API base URL |
| `TEST_EVIDENCE_ROOT` | optional | Paperclip Agent environment | Transient local output root, never committed |

NightWatch must map `LUMI_API_BASE_URL` internally to the selected environment's `base_url_env`. Paperclip must not maintain separate competing `NW_*_BASE_URL` values for the same Lumi endpoint.

## Secret bindings

Common credential references include:

- `NW_TESTED_API_TOKEN`
- `DEVICE_SECRET_B64URL`
- `USER_ACCOUNT` and `USER_PASSWORD`
- `OPERATOR_ACCOUNT` and `OPERATOR_PASSWORD`
- `GITHUB_TOKEN` for approved private-repository reads or Finding publication

Only the variables required by the selected auth profile may be leased to the executor. Report missing names, never values. Do not read `*.local.json`, `.env`, shell history, another Agent's configuration or a developer Keychain as fallback.

The D0 definition, Case set, deployed subject digest and DeploymentReceipt are Task inputs, not environment variables.
