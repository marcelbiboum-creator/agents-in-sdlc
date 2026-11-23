---
title: "第 6 课——使用 Playwright MCP 验证功能"
description: "在 Copilot CLI 中检查或配置 Playwright MCP，并使用它在浏览器中探索筛选功能。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

正如前面所强调的，编写代码不仅仅是写代码。我们需要处理数据、外部服务，还要让 Copilot 能使用额外的自动化功能。这里就要用到 MCP 服务器。MCP 服务器让 Copilot 超越 CLI 内置功能，为它提供更多工具和服务。

在本课中，你将：

- 理解模型上下文协议（MCP），以及 Copilot CLI 如何使用它。
- 尚未提供时添加 Playwright MCP 服务器。
- 请智能体驱动浏览器并探索筛选功能。

## 场景

单元测试和端到端测试固然重要，但验证界面更新需要实际与界面交互。你希望允许 Copilot像用户一样使用正在开发的网站，以进一步自动化更改并提升对更新行为符合预期的信心。

## 什么是模型上下文协议（MCP）？

[模型上下文协议（MCP)][mcp-blog-post]为 AI 智能体提供与外部工具和服务通信的方式。通过 MCP，AI 智能体可以实时与外部工具和服务通信，从而获取最新信息并代表你执行操作。

这些工具和资源通过 MCP 服务器访问；MCP 服务器充当 AI 智能体与外部工具和服务之间的桥梁。每个 MCP 服务器代表 AI 智能体可访问的一组不同工具和资源。

一些常见的 MCP 服务器包括：

- **[GitHub MCP Server][github-mcp]**：提供管理 GitHub 仓库、议题和拉取请求所需的 API 访问。
- **[Playwright MCP Server][playwright-mcp-server]**：使用 Playwright 提供浏览器自动化能力。

还有许多其他 MCP 服务器可用。GitHub 提供 [MCP registry][mcp-registry]，以提高生态系统的可发现性和贡献便利性。

> [!CAUTION]
> 使用 MCP 服务器时，应将其视为项目中的其他依赖项。使用前请审查源代码、验证发布者，并考虑安全影响。

## 添加 Playwright MCP 服务器

如果 Playwright MCP 服务器尚不可用，请添加它，以便 Copilot 能像用户一样与网站交互。

> [!NOTE]
> 如果已在 Copilot CLI 中配置 Playwright MCP，请跳过这些设置步骤，继续下一部分。

1. 返回 Codespace。
2. 在 Copilot CLI 中输入以下命令，打开添加 MCP 服务器对话框：

   ```plaintext
   /mcp add
   ```

3. 在名称处输入 `playwright`，然后按 <kbd>Tab</kbd>。
4. 按 <kbd>Enter</kbd>确认服务器类型为 **STDIO**，再按 <kbd>Tab</kbd>。
5. 在 **Command** 对话框中粘贴以下内容：

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. 按 <kbd>Control</kbd>+<kbd>S</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>S</kbd>（Windows/Linux）保存新 MCP 服务器。
7. 按 <kbd>Esc</kbd>退出 MCP 对话框。

## 请 Copilot 使用 Playwright 探索功能

之前你已手动确认功能符合预期。现在使用 Copilot 提供的 Playwright MCP 服务器执行相同验证！

1. 使用以下提示，请 Copilot 使用 Playwright MCP 验证功能：

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> 实际上不必明确要求 Copilot 使用 MCP 服务器，因为它通常会自行判断。但既然你知道应使用哪个工具，适当地指引方向也无妨！这有助于获得更一致的结果，并节省一些令牌。

2. 观察 Copilot 列出在浏览器中执行的各个步骤，以确认功能正常。
3. 阅读报告并确保一切符合预期。

Copilot 将启动服务器、使用 Playwright 与网站交互、停止服务器，并提供报告。

## 总结与后续步骤

恭喜，你已使用 Playwright MCP 服务器，在 Copilot CLI 中通过真实浏览器探索功能！回顾一下，你：

- 学习了模型上下文协议（MCP）以及 Copilot CLI 如何使用它。
- 尚未提供时添加了 Playwright MCP 服务器。
- 请智能体驱动浏览器并探索筛选功能。

接下来，你将[创建 QA 自定义智能体][next-lesson]，在专用角色中结合技能和浏览器工具。

## 资源

- [什么是 MCP，为什么大家都在讨论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [向 Copilot CLI 添加 MCP 服务器][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
