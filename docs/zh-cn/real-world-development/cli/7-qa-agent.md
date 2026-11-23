---
title: "第 7 课——创建并使用 QA 智能体"
description: "创建一个 QA 自定义智能体，将议题需求、quality-checks 技能和 Playwright MCP 结合起来。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已经使用 `quality-checks` 技能运行自动化检查，并通过 Playwright MCP 在浏览器中观察筛选体验。现在将这些能力整合到具有明确 QA 流程的自定义智能体中。

在本课中，你将：

- 探索自定义智能体如何与指令、技能和 MCP 工具协作。
- 创建并检查可复用的质量保证配置。
- 选择 QA 智能体，并根据筛选议题审查其发现。

## 场景

Tailspin Toys 希望在打开拉取请求（PR）前，针对需求、代码质量、自动化检查、测试覆盖率和浏览器行为进行一致审查。自定义智能体可以协调该 QA 流程，并提供可复用的报告。

## 什么是自定义智能体？

自定义智能体是在 Markdown 配置文件中定义的 Copilot 专用版本。该配置描述智能体的用途、指令和可用工具。在本研讨会中，你将在 `.github/agents/qa.agent.md`中定义 QA 角色，并在 Copilot CLI 中选择它。

你使用过的自定义功能各司其职：仓库指令描述团队标准；`quality-checks` 技能封装可重复的检查；Playwright MCP 提供浏览器工具；QA 配置告诉 Copilot 如何使用这些能力评估需求并报告发现。它不会替代这些功能，也不需要另一个对话。

## 创建 QA 配置

打开功能 PR 前，请 Copilot 创建可复用的 QA 配置。该配置将定义 QA 执行的检查以及必须遵守的边界。

1. 返回 Codespace，并确认筛选对话处于 Interactive 模式。
2. 请默认智能体创建新的自定义智能体：

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## 检查配置

使用新智能体之前，请审查其配置，以确认 Copilot 已捕获预期的 QA 工作流和边界。这可以防止不完整或范围过大的智能体在你只想验证功能时修改功能。

1. 输入 `/diff`并打开 `.github/agents/qa.agent.md`。
2. 阅读 frontmatter。`description`是必需的；`name`是可选的，但包含它会提供清晰的显示名称。
3. 阅读配置指令，确认 QA 从需求出发、遵循仓库指令、运行 `quality-checks` 技能并使用 Playwright MCP。
4. 确认 QA 会报告支持证据，在更改实现代码前询问，并且不会提交更改或打开拉取请求。
5. 如果生成的配置遗漏了这些职责或边界，请在继续前请默认智能体修改。

## 针对议题运行 QA

Copilot CLI 在对话开始时加载项目智能体。创建配置后恢复同一个筛选对话，然后选择 QA，让它使用上下文中已有的议题和规划决策。

1. 使用以下提示启用智能体：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 由于刚创建智能体，它可能不会出现在可用智能体列表中。它确实存在，上面的命令会激活它。

2. 使用以下提示，请 QA 智能体审查功能：

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA 智能体开始工作！
4. 完成后阅读它提供的报告！

## 总结与后续步骤

你已在工作流中添加可复用的专用角色，并审查了其工作。在本课中，你：

- 探索了自定义智能体如何与指令、技能和 MCP 工具协作。
- 创建并检查了可复用的质量保证配置。
- 选择了 QA 智能体，并根据筛选议题审查了其发现。

现在，实现、技能更新、QA 配置、测试和验证报告已准备好接受审查。接下来，你将[将它们整合到功能 PR 中，并使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义智能体][create-agents]
- [自定义智能体配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
