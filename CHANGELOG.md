# 版本记录

## 0.3.0 - 2026-09-03

- 重新定义 APP 测试与 API 测试岗位，补齐 Task 输入、环境输入、三类工作模式、协作路由和完成条件。
- 明确项目目标、地址、版本、Case 和授权只能由 Paperclip Task 或 Agent 环境导入，禁止从工具仓历史默认值推断。
- 明确 Secret 仅通过 Paperclip Secret Reference 注入，Task 只能传递凭证引用。

## 0.2.0 - 2026-09-03

- 增加组织级 `lumi-ai-native-delivery` Skill 和机器可读交付 Workflow。
- 固化“意图/合同 → 计划 → 自测 → 独立验证 → PR/main/CI/OCI → 授权部署 → 生产验收 → 反馈改进”闭环。
- 明确 Paperclip 只负责状态、责任和证据索引，各类权威产物仍由对应真源保存。
- 为 APP/API 测试岗位增加独立验证、错误分诊、状态防漂移和反馈回流 Eval。

## 0.1.0 - 2026-09-03

- 建立 APP 测试工程师与 API 测试工程师的正式 Agent 定义。
- 建立 Prismloop、NightWatch 工具使用 Skill 和共享测试 Case 治理 Skill。
- 固化 Agent、工具、Case 三条独立迭代线及测试回执版本要求。
