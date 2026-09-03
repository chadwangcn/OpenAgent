# OpenAgent

OpenAgent 管理 Lumi 数字员工的可版本化定义。Paperclip 负责运行这些员工、派发任务和保存协作回执；OpenAgent 负责回答“这个员工是谁、会什么、依赖什么、如何工作、如何评估”。

## 目录

```text
agents/       岗位定义、短版 AGENTS.md、Workflow、Eval
skills/       可导入 Paperclip Company Skill Library 的 Agent Skills
workflows/    跨岗位、跨阶段的组织级交付 Workflow
organization.yaml  当前数字组织版本与运行绑定
CHANGELOG.md  Agent 产品版本记录
```

首批测试员工：

- `app-test-engineer`：使用 Prismloop 执行 Figma 驱动的 APP 真机/云手机测试。
- `api-test-engineer`：使用 NightWatch 执行 D0 API 定义驱动的黑盒测试。

测试 Case 与工具代码分别在 Prismloop、NightWatch 中维护。本仓不保存真实环境变量值或运行证据。

## 协作模型

Lumi 使用非线性的 AI-native SDLC 闭环：意图与合同、实施计划、源码与自测、独立验证、
PR/main/CI/OCI、授权部署、生产验收、运行反馈逐级产生可验证产物。Paperclip 保存任务状态、
责任人和证据索引；Git、Figma、OCI Registry、部署回执和测试仓分别保存各自权威产物。

所有交付岗位共享 `lumi-ai-native-delivery` Skill。它不替代各仓 `AGENTS.md`、D0 合同或
具体工具 Skill，而是统一阶段门、阻塞分诊、状态语义和反馈回流规则。
