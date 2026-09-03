# OpenAgent Repository Instructions

本仓库是 Lumi 数字员工的定义、Skill、Workflow 与能力评估真源。进入本仓的 Agent 必须先读取本文件，再读取目标员工目录中的 `AGENTS.md`。

## 边界

- `agents/` 定义岗位、输入输出、环境契约、Skill 组合、Workflow 和 Eval。
- `skills/` 只描述可复用的操作能力，不复制工具项目内部实现。
- Prismloop、NightWatch 等工具代码及测试 Case 不在本仓维护；这里只保存依赖名称、版本约束和调用契约。
- Paperclip 是运行与任务控制面。Agent 定义先在本仓版本化，再导入 Paperclip；禁止只在 UI 中维护一份不可追踪的长期定义。
- 不保存 Token、账号密码、设备密钥、云平台 AK/SK、临时签名 URL、原始日志或用户数据。

## 三条迭代线

1. Agent 迭代：修改本仓 Agent 定义、Skill、Workflow 或 Eval。
2. 工具迭代：修改对应工具仓库的运行能力、协议或稳定性。
3. Case 迭代：修改对应测试仓库的 `cases/`，不得与工具实现混在同一 PR。

每次测试回执必须固定 Agent、Skill、工具和 Case 四个版本。任务执行授权不自动授权修改工具、Case、生产环境或被测业务代码。

