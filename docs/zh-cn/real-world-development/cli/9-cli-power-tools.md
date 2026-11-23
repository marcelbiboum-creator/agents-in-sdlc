---
title: "第 9 课——GitHub Copilot CLI 中的斜杠命令"
description: "探索用于管理上下文、选择模型、共享会话和可选云委派的斜杠命令。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

与优秀的 CLI 工具一样，GitHub Copilot CLI 提供许多斜杠命令用于交互。这些命令公开高级功能、幕后信息和额外配置选项。你已经使用过 `/diff`、`/mcp`、`/skills`、`/agent`和 `/pr`等命令。下面探索一些其他实用命令。

在本课中，你将：

- 使用 `/context`和 `/compact`探索 Copilot 如何管理对话上下文。
- 使用 `/model`探索可用模型。
- 了解 `/share`如何导出或共享会话。
- 探索用于并行工作、工作树和委派给云智能体的可选命令。

## 场景

核心 CLI 工作流已经完成。现在来看几个附加能力：管理上下文、切换模型、共享会话，以及可选地将工作委派给 [Copilot 云智能体][about-cloud-agent]。

## 探索 Copilot CLI 上下文

处理较大或较复杂任务时，可能会达到模型的最大上下文窗口。Copilot CLI 会在需要时自动压缩对话，你也可以使用斜杠命令自行检查或压缩。

1. 返回 Codespace。如果 Copilot CLI 尚未打开，请从仓库根目录启动。
2. 输入：

   ```plaintext
   /context
   ```

3. 注意模型、当前令牌用量，以及上下文在系统指令、工具、消息和可用空间之间的分布。
4. 压缩对话：

   ```plaintext
   /compact
   ```

5. 再次输入 `/context`并比较结果。如果对话已经很小，变化可能不明显。

> [!NOTE]
> 上下文窗口接近上限时，Copilot CLI 会自动压缩。希望自行选择压缩时机时，请使用 `/compact`。切换到不相关任务并希望全新对话时，请使用 `/clear`或 `/new`。

## 选择模型

不同模型具有不同优势，开发者的偏好也不同。Copilot CLI 允许列出并选择要使用的模型。

1. 输入：

   ```plaintext
   /model
   ```

2. 浏览可用模型及使用信息。
3. 保持当前模型、选择另一个模型，或按 <kbd>Esc</kbd>关闭列表。

## 共享会话

团队协作和分享经验有助于所有人提升 AI 工具的使用水平。`/share`命令可以将会话导出为 Markdown 或 HTML 文件、创建可共享链接或发布 GitHub gist。

1. 输入 `/help`并查看已安装版本中的 `/share`选项。
2. 如果要共享会话，请选择符合需求的目标，例如使用 `/share file`导出本地 Markdown 文件。
3. 在发送给任何人或发布之前，请审查导出的内容。会话导出可能包含提示、响应和项目详情。

发布链接或 gist 是可选操作。不要发布团队无意共享的仓库或对话内容。

## 可选：横向扩展或委派

核心研讨会已完成。Copilot CLI还提供适用于更大型任务的命令：

- `/fleet`可以将独立子任务分配给子智能体并并行运行。
- `/worktree`可以为独立任务创建隔离的 Git 工作树。
- `/delegate`可以将任务发送给 Copilot 云智能体，它会异步工作并可能打开拉取请求。

这些命令是可选的，因为它们可能创建额外工作树或远程工作。尝试前，请先启动一个全新且范围明确的任务，并通过常规工作流审查结果。如果想深入了解异步智能体工作，请继续学习[云智能体研讨会][cloud-workshop]。

## 总结与后续步骤

使用 Copilot CLI 中的斜杠命令，可以进行配置、共享会话，并查看幕后情况。在本课中，你：

- 使用 `/context`和 `/compact`探索了 Copilot 如何管理对话上下文。
- 使用 `/model`探索了可用模型。
- 学习了 `/share`如何导出或共享会话。
- 探索了用于并行工作、工作树和委派给云智能体的可选命令。

Copilot CLI 中还有更多斜杠命令等待探索！现在，[回顾所学内容][next-lesson]并了解继续学习的一些后续步骤，结束本次旅程。

## 资源

- [Copilot CLI 命令参考][cli-reference]
- [Copilot CLI 上下文管理][context-management]
- [关于 Copilot 云智能体][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
