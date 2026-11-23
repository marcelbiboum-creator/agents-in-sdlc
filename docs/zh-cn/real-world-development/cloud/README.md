---
slug: zh-cn/real-world-development/cloud
title: "GitHub Copilot 云智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[GitHub Copilot 云智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent) 允许 GitHub Copilot 在云端异步工作。你在 GitHub 上分配任务，云智能体会在后台获取任务、探索仓库、修改文件并打开拉取请求，因此你可以继续处理其他工作。

在以下练习中，你将添加云智能体遵循的自定义指令，分配一个 GitHub议题并让它实现该工作。你将审查并使用自定义智能体来塑造其工作方式，在智能体仪表板中监控和引导会话，最后审查其拉取请求并迭代处理结果。

## 练习

| 练习 | 主题 | 描述 |
|----------|-------|-------------|
| [0. 先决条件][ex0] | 设置 | 创建仓库和 Codespace |
| [1. 自定义指令][ex1] | 上下文 | 添加云智能体遵循的自定义指令 |
| [2. 云智能体][ex2] | 异步智能体 | 将议题分配给 GitHub Copilot 云智能体 |
| [3. 自定义智能体][ex3] | 专用智能体 | 审查并使用自定义智能体 |
| [4. 管理智能体][ex4] | 监控 | 监控并引导智能体会话 |
| [5. 迭代][ex5] | 审查 | 审查拉取请求、迭代 Copilot 的工作并选择后续步骤 |

## 先决条件

参加本研讨会前，请确保：

- [ ] 已拥有 GitHub 帐户，并已启用有效的 **Copilot Student、Pro、Pro+、Business 或 Enterprise** 计划
- [ ] 已为你的帐户或组织启用 Copilot 云智能体

> [!TIP]
> 没有付费计划？通过 [GitHub Education][callout-student-plan-education]，已验证的学生可以免费使用 GitHub Copilot。**Copilot Student** 计划包含本研讨会使用的智能体、MCP、代码审查和 Copilot CLI 功能，因此你可以完成所有流程。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> 云智能体适用于 **Copilot Student、Pro、Pro+、Business 和 Enterprise**；除 Copilot Free 外，所有计划均可使用。在 Copilot Business 或 Enterprise 中，管理员必须为组织启用该功能。

> [!NOTE]
> 本流程不涉及 MCP。如需探索如何通过 Copilot 使用 MCP 服务器，请参阅 [CLI 流程](../cli/)或 [VS Code 流程](../vscode/)。

## 开始

**[从练习 0：先决条件开始 →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
