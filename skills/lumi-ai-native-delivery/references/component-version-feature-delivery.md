# 版本化组件交付参考

适用于 SDK、APP、后端、设备平台、Console 和测试工具等有版本化源码交付的仓库。组件仓
拥有版本/Feature 任务真源；D0 只拥有跨系统合同和中央 Case；Paperclip 只拥有控制面状态
和回执索引。

## 工作单元

```text
repository + target_version + feature_id + request_class + contract_or_design_pin
```

先按该指纹查找未关闭 Paperclip Task；同一交付复用原任务。每个活跃写任务只允许：

- 一个目标仓库；
- 一个 Feature 分支 `feature/<version>-<short-name>`；
- 一个从精确 `origin/main` commit/tree 创建的干净独立 worktree；
- 一个 PR 和一个不可变候选。

多个需求 ID 可以在同一 PR 中实现，但只能有一个实际分支和候选，并在 PR/Receipt 中列出
全部 Case 映射。前置 Feature 合入 main 后，后续 Feature 必须从新的 main 重建 baseline。

## 默认门禁

```text
planned/blocked
-> baseline recorded + clean worktree
-> implementation + self-test
-> PR + independent review/test
-> merge main + post-merge regression
-> profile-specific candidate and acceptance
-> immutable tag/release when applicable
```

自测、CI、PR 或 Agent running 都不是终止证据。独立验证针对精确 source commit 和候选 SHA。
失败通过原任务 ReworkRequest 返回实施，不创建平行任务。无有效 Receipt 的长时间运行记录为
`stalled_runtime`，由运行面负责人处理。

## Release profile

服务使用 OCI digest、SRE 授权部署和运行时 digest 回读；客户端库使用版本化包/AAR、
checksum、API inventory、consumer 和真实设备/服务证据，不产生 OCI。文档和测试工具按各自
构建/发布形态定义候选，不得套用服务端发布门。

回执永远不得含 Secret、Token、设备凭证、完整签名 URL、原始媒体或用户内容。
