---
title: "第 8 课——创建并合并功能 PR"
description: "统一审查筛选、指令、技能更新、QA 配置和测试，然后创建 PR 并使用 Agent Merge。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

筛选实现、指令更新、技能更新、质量保证（QA）配置和测试都保存在同一个分支上。现在可以统一审查并打开拉取请求。星级评分的拉取请求（PR）由你亲自合并；这次将允许 **Agent Merge**管理流程。

> [!NOTE]
> 通常，我们会把功能、指令更新、技能更新和 QA 智能体拆分到几个独立 PR 中。为简化研讨会，我们将完整的筛选和质量工作流保留在同一个对话和分支中，全部交付到这个 PR。

在本课中，你将：

- 了解 Agent Merge及其如何自动化合并生命周期。
- 检查完整功能更改和验证证据。
- 创建筛选 PR。
- 仅在审查后启用 Agent Merge，并确认 PR 已合并。

## 场景

在整个筛选工作流中，你使用 Copilot 规划、实现并验证功能。Tailspin Toys 希望自动化剩余的 PR 工作，同时将合并授权留在开发人员控制之下。

## Agent Merge简介

**Agent Merge**自动化完成拉取请求所需的剩余工作。启用后，Copilot 会处理阻碍 PR 的问题——修复失败的持续集成（CI）检查、回复审查评论，并在需要时变基——然后在仓库允许时启用 GitHub 自动合并。

到目前为止，你一直亲自选择 **Merge pull request**。Agent Merge 可以接手这项职责。在启用前，请审查工作并决定它是否已经就绪。

## 使用 Agent Merge管理 PR

所有代码已创建完毕，现在统一审查、创建 PR，并让 Agent Merge管理剩余流程。

1. 返回 Codespace。
2. 输入 `/agent`打开智能体对话框。
3. 从选项列表中选择 **Default**，然后按 <kbd>Enter</kbd>。
4. 使用命令 `/pr create`创建新 PR。
5. 使用 `/pr agentmerge`激活 Agent Merge。
6. Copilot 将监控 PR 上的持续集成过程。全部成功后，它会执行合并。
7. 确保看到 Copilot 发出的类似于“PR #14 was squash-merged successfully.”的消息。

> [!IMPORTANT]
> Agent Merge不会绕过必需审批、分支保护、合并队列、仓库设置或缺失权限。如果流程受阻，请阅读报告原因，并在仓库允许时手动完成已审查的合并。

## 总结与后续步骤

你已自动化开发流程中的多个环节，包括生成代码、测试和验证代码，以及拉取请求流程。你：

- 了解了 Agent Merge及其如何自动化合并生命周期。
- 检查了完整功能更改和验证证据。
- 创建了筛选 PR。
- 仅在审查后启用 Agent Merge，并确认 PR 已合并。

接下来，你将[探索更多实用的 Copilot CLI 斜杠命令][next-lesson]，以管理上下文、模型、会话共享和可选的云委派。

## 资源

- [使用 Copilot CLI 管理拉取请求][manage-prs]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
