---
title: "练习 3——使用 Playwright MCP服务器测试功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：智能体模式][previous-lesson] · [下一课：自定义智能体 →][next-lesson]

你刚使用智能体模式构建了筛选功能。在打开拉取请求前，应确认它在浏览器中确实有效。无需亲自逐项点击应用，而是连接 **Playwright MCP服务器**，让 Copilot驱动真实浏览器测试功能，然后发布分支并打开 PR。

在本练习中，你将：

- 了解模型上下文协议（MCP），以及 MCP服务器如何为 Copilot提供新工具。
- 将 Playwright MCP服务器添加到工作区。
- 请 Copilot使用它在浏览器中手动测试筛选功能。
- 发布分支并为筛选工作打开拉取请求。

## 什么是模型上下文协议（MCP）？

智能体模式可以超越编辑器访问外部资源时，会变得更强大。模型上下文协议（MCP）正是 Copilot实现这一点的方式；它是智能体与外部工具和服务通信的标准方式。

![智能体模式内部工作及其与上下文、LLM和工具（包括 MCP服务器与 VS Code扩展提供的工具）交互的示意图](../../../_images/ex1-mcp-diagram.png)

[模型上下文协议（MCP）](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/)为 AI智能体提供与外部工具和服务通信的方式。通过 MCP，AI智能体可以实时与外部工具和服务通信，从而获取最新信息（使用资源），并代表你执行操作（使用工具）。

这些工具和资源通过 MCP服务器访问；MCP服务器充当 AI智能体与外部工具和服务之间的桥梁。MCP服务器负责管理 AI智能体与外部工具（例如现有 API或 NPM包等本地工具）之间的通信。每个 MCP服务器代表一组不同的工具和资源，AI智能体可访问它们。

常见 MCP服务器包括：

- **[GitHub MCP服务器](https://github.com/github/github-mcp-server)**：提供管理 GitHub仓库的 API。它允许 AI智能体创建新仓库、更新现有仓库，以及管理议题和拉取请求。
- **[Playwright MCP服务器](https://github.com/microsoft/playwright-mcp)**：使用 Playwright提供浏览器自动化能力，可导航网页、填写表单和选择按钮。

还有许多其他 MCP服务器可提供不同工具和资源。GitHub提供 [MCP registry](https://github.com/mcp)，以提高生态系统可发现性和贡献便利性。

> [!CAUTION]
> 从安全角度，应像对待项目中的其他依赖项一样对待 MCP服务器。使用前，请仔细审查源代码、验证发布者，并考虑安全影响。只使用可信 MCP服务器，并谨慎授予敏感资源或操作的访问权限。

## 审查 MCP配置

`.vscode/mcp.json`文件配置此 VS Code工作区可用的 MCP服务器。

1. 在 Codespace中打开 `.vscode/mcp.json`。
2. 应看到已为你配置的 `github`服务器：

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        }
      }
    }
    ```

项目模板已附带此 `github`条目，因此 Copilot能读取前一练习中的待办事项议题。它使用[远程 GitHub MCP服务器][remote-github-mcp-server]，无需本地安装；VS Code通过 HTTP连接，并在 Copilot首次使用其工具时要求你进行 GitHub身份验证。

## 添加 Playwright MCP服务器

现在添加第二个服务器。[Playwright MCP服务器][playwright-mcp-server]为 Copilot提供可控制的浏览器，正是测试功能所需。

1. 在 `.vscode/mcp.json`中，和 `github`并列添加 `playwright`条目，使文件如下：

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        },
        "playwright": {
          "command": "npx",
          "args": ["@playwright/mcp@latest", "--headless"]
        }
      }
    }
    ```

2. 保存文件。

与远程 `github`服务器不同，`playwright`是**本地**服务器：VS Code通过运行 `npx @playwright/mcp@latest`在你的机器上启动它。`--headless`标志要求 Playwright在无可见窗口的情况下运行浏览器，这是 Codespace中无桌面环境时必需的。

> [!NOTE]
> Tailspin Toys项目已使用 Playwright进行端到端测试，因此 Playwright所需的浏览器通常已经安装。如果 Copilot稍后报告缺少浏览器，请让它运行 `npx playwright install chromium`后重试。

## 启动并信任服务器

VS Code按需启动 MCP服务器：首次需要某个服务器的工具时，VS Code会启动服务器并要求确认信任。

1. 在 `.vscode/mcp.json`中，`playwright`条目上方会出现 **Start**操作。选择它立即启动服务器，并确认配置正确。
2. 如果 VS Code要求确认是否信任服务器，请审查配置并选择信任，以便服务器启动。

手动启动是可选的；如果跳过，下一步 Copilot首次需要工具时，VS Code会启动服务器并提示信任。

## 测试筛选功能

[Playwright MCP服务器][playwright-mcp-server]为 Copilot提供可驱动的真实浏览器。无需亲自点选应用，智能体可以打开页面、导航、应用筛选，并向你报告结果，然后总结观察结果。这是在不离开对话的情况下确认功能符合预期的最快方式。

底层中，Playwright MCP服务器使用页面的[无障碍树][playwright-mcp-server]而不是截图。也就是说，智能体会像辅助技术一样处理结构化、带标签的元素（按钮、链接、列表项）；一次快速功能检查同时也能作为轻量无障碍检查。

服务器已连接且应用正在运行后，请 Copilot测试刚构建的筛选功能：

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot将通过 Playwright MCP服务器启动浏览器、逐步执行，并报告结果。请将摘要与议题中的验收标准进行比对；若发现异常，请提出后续问题或将任务退回修复代码，再打开拉取请求。

> [!NOTE]
> 此测试要求应用运行在 `http://localhost:4321`。如果已停止开发服务器，请先启动，再发送提示。首次使用 Playwright MCP服务器时，Copilot可能需要下载浏览器；如果报告缺少浏览器，请让它运行 `npx playwright install chromium`后重试。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## 发布分支并创建拉取请求

确认功能正常后，即可打开拉取请求（PR）供团队审查。第一步是发布 `filtering-vscode`分支。

1. 在 Codespace中导航到 **Source Control**面板，并审查 Copilot修改的更改。
2. 选择 **+**图标暂存更改。
3. 使用 **Sparkle**按钮生成提交消息。

   ![Source Control面板中显示更改的截图](../../../_images/ex3-source-control-changes.png)

4. 选择 **Publish**将分支推送到仓库。

## 创建拉取请求

可以通过 github.com、GitHub 命令行界面（CLI）等方式创建 PR。既然已经在使用 GitHub Copilot，就让它代为创建 PR！它可以找到相关议题并将 PR关联到议题。

1. 导航到 Copilot Chat面板并选择 **New Chat**开始新会话。
2. 确信智能体下拉列表中已选择 **Agent**，以便 Copilot使用 GitHub工具。
3. 请 Copilot创建 PR：

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. 根据需要选择 **Continue**，允许 Copilot收集信息并执行操作。首次使用 GitHub工具时可能提示 GitHub身份验证，请按照提示授权。
5. 注意 Copilot如何搜索议题、找到正确议题并创建 PR。
6. 选择 Copilot生成的链接审查拉取请求，但暂时**不要合并**。

## 总结与后续步骤

恭喜！在本练习中，你：

- 了解了模型上下文协议（MCP），以及 MCP服务器如何为 Copilot提供新工具。
- 将 Playwright MCP服务器添加到工作区。
- 使用它在发布前于浏览器中手动测试筛选功能。
- 发布了分支并为筛选工作打开了拉取请求。

你使用 MCP服务器测试了功能，但 MCP只是扩展 Copilot的一种方式。接下来，[创建自定义智能体][next-lesson]以简化无障碍审查等聚焦任务。

## 资源

- [什么是 MCP，为什么大家都在讨论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP Registry][mcp-registry]
- [VS Code中的 MCP服务器][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
