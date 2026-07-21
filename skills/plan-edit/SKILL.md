---
name: plan-edit
description: Create or revise project implementation plans as Markdown files in .agents/plans. Use when the user asks to create a plan, write a plan, revise an existing plan, or generate an implementation plan.
---

# Plan Edit

## 适用场景

当用户要求：
- 创建/编写/生成项目计划
- 修订/更新已有 plan 文件
- 根据需求生成带步骤的实施方案

## 工作流程

1. 收集需求：明确计划标题、目标、范围、约束与关键文件。
2. 确定目标目录：当前项目根目录下的 `.agents/plans/`。
3. 如果是**创建**：
   - 生成文件名：`${yyMMddHHmm}_${title}.plan.md`，其中 `yyMMddHHmm` 为当前本地时间。
   - 直接写入 `.agents/plans/`。
4. 如果是**修订**：
   - 读取用户指定的已有 plan 文件。
   - 保留原有结构，仅修改用户要求的部分。
   - 按用户指示决定是否更新时间戳或保留原文件名。
5. 编写 plan 内容，必须包含以下章节：
   - 标题
   - 概述
   - 目标
   - 实施步骤（编号列表，每项带 `- [ ]` checkbox，并附实施方案）
   - 关键文件
   - 风险与注意事项
6. 写入文件并返回最终文件路径。

## Plan 模板

```markdown
# [标题]

## 概述
[一句话说明计划要解决什么问题]

## 目标
- [目标 1]
- [目标 2]

## 实施步骤

1. [ ] [步骤标题]
   - 实施方案：
     - [具体动作]
     - [具体动作]

2. [ ] [步骤标题]
   - 实施方案：
     - [具体动作]

## 关键文件
- `[文件路径]`

## 风险与注意事项
- [风险 1]
- [风险 2]
```

## 修订规则

- 不得删除未要求修改的章节或步骤。
- 若用户未指定新文件名，保留原文件名。
- 若用户希望基于当前计划创建新版本，则生成新的时间戳文件名。