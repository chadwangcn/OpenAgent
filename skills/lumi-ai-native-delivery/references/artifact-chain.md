# Artifact chain reference

| Stage | Required artifact | Authority |
| --- | --- | --- |
| Intent | IntentRecord | request originator / product owner |
| Contract or design | pinned D0 definition or Figma version | contract or design owner |
| Dispatch | WorkPackage and DispatchReceipt | PM |
| Implementation | source commit/tree, SelfTestReceipt, DeliveryNotice | component/tool Owner |
| Independent check | ReviewReceipt or TestRunReceipt | named reviewer/test engineer |
| Release candidate | PR, main readback, CI run, OCI digest | GitHub and registry |
| Deployment | authorization, DeploymentReceipt, runtime digest | human authority and SRE |
| Acceptance | AcceptanceNotice with external I/O/business evidence | named independent acceptor |
| Learning | ImprovementCandidate and regression eval/Case | lane owner |

Paperclip holds status, assignments and links. It is not the source of truth for Git commits, OCI digests, deployment state, Figma designs or test artifacts.
