---
name: plan-implement
description: Implement a project plan by executing its numbered steps and checking off completed items. Use when the user asks to implement a plan, execute plan steps, run a plan file, or complete tasks from a plan.
---

# Plan Implement

## 适用场景

当用户要求：
- 实施/执行某个 plan 文件
- 完成计划中的部分或全部步骤
- 按编号执行指定步骤

## 参数

1. `plan_file`：plan 文件路径（必填）。
2. `steps`（可选）：步骤编号，多个用逗号或空格分隔。例如 `1,3,5` 或 `1 3 5`。未指定时执行全部未勾选步骤。

## 工作流程

1. 读取 `plan_file` 文件内容。
2. 解析所有带 checkbox 的编号步骤：
   - 步骤编号以 Markdown 有序列表数字为准。
   - checkbox 形式为 `- [ ]` 或 `- [x]`。
3. 如果指定了 `steps` 参数，仅保留对应编号的步骤。
4. 默认跳过已勾选（`- [x]`）步骤，除非用户明确要求重新执行。
5. 按顺序执行每个待实施步骤：
   - 严格遵循该步骤中"实施方案"的说明。
   - 如需调用工具，按说明顺序执行。
   - 每一步完成后，将该步骤的 checkbox 从 `- [ ]` 改为 `- [x]`。
   - 保存文件。
6. 若执行过程中出现错误，停止并报错，不再继续后续步骤。
7. 完成所有步骤后，简要汇报执行结果与更新的 checkbox 状态。