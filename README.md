# OpenAgent

OpenAgent 管理 Lumi 数字员工的可版本化定义。Paperclip 负责运行这些员工、派发任务和保存协作回执；OpenAgent 负责回答“这个员工是谁、会什么、依赖什么、如何工作、如何评估”。

## 目录

```text
agents/       岗位定义、短版 AGENTS.md、Workflow、Eval
skills/       可导入 Paperclip Company Skill Library 的 Agent Skills
organization.yaml  当前数字组织版本与运行绑定
CHANGELOG.md  Agent 产品版本记录
```

首批测试员工：

- `app-test-engineer`：使用 Prismloop 执行 Figma 驱动的 APP 真机/云手机测试。
- `api-test-engineer`：使用 NightWatch 执行 D0 API 定义驱动的黑盒测试。

测试 Case 与工具代码分别在 Prismloop、NightWatch 中维护。本仓不保存真实环境变量值或运行证据。

