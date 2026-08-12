---
name: pull-request-rules
description: Handle GitHub Issue and Pull Request creation safely. Use when the user asks to open, create, file, or submit a GitHub issue or pull request, or when work is about to create one on the user's behalf.
---

# Pull Request 操作

## 工作流程

1. 确认目标仓库、操作类型（Issue 或 Pull Request）以及用户希望提交的内容。
2. **先查重**：在目标仓库中搜索相似的 issue/PR，覆盖标题、正文关键词、相关文件或功能范围。
   - 如果发现相似项，停止创建操作。
   - 向用户报告相似项的编号、标题、状态和链接，并等待用户确认下一步。
3. **读取仓库约定**：检查目标仓库提供的 issue/PR 模板、贡献指南、标签约定以及其他必填元数据。
4. 根据模板和仓库约定整理提交内容，补齐必填章节、标签、assignee、milestone 等元数据；无法确定的字段先向用户确认。
5. 只有在查重未发现相似项，且模板与必填元数据已确认后，才创建 Issue 或 Pull Request。
6. 创建后返回链接、编号、实际使用的模板和元数据；若平台或权限阻止创建，明确报告阻塞原因，不声称已创建。

## 硬性边界

- 查重结果存在相似项时，创建动作必须暂停，不能直接创建重复的 Issue 或 Pull Request。
- 必须遵循目标仓库的相应模板；模板要求与用户指令冲突时，先说明冲突并请求确认。
- 标签和其他预设元数据必须使用目标仓库支持的值，不凭空臆造。
- 创建前检查和创建动作都应针对用户指定的目标仓库，不能因仓库名称相似而自行切换目标。

## 完成标准

操作仅在以下条件同时满足时视为完成：查重已完成且无待确认的相似项、目标仓库模板和必填元数据已应用、Issue 或 Pull Request 已成功创建并返回可验证的链接；若任一条件不满足，报告当前状态和阻塞点。
