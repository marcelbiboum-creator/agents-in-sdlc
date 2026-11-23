---
title: "练习 2——使用 Copilot 智能体模式添加新功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

应用中最简单的更新通常也需要修改多个文件并执行测试。作为开发人员，你的流程通常包括查找全部相关文件、进行更改、运行测试、调试、找出遗漏的文件，再次更新……如此循环。

这正是 Copilot 智能体模式发挥作用的地方。

Copilot 智能体模式可以在 IDE中更自主地工作。它的行为类似开发人员：先探索现有项目结构，再执行必要更新，运行测试等任务，并自动修复发现的问题。下面探索如何使用智能体模式为网站引入新功能。

> [!NOTE]
> 虽然名称相似，智能体模式和云智能体面向两种不同体验。智能体模式在 IDE中执行任务，反馈周期短且可直接交互。云智能体更像异步工作的结对开发人员，通过议题和拉取请求与你协作。

在本练习中，你将了解：

- Copilot 智能体模式如何探索项目、识别相关文件并进行协调更改。
- GitHub Copilot 智能体模式如何在界面和数据层中实现新功能。
- 如何在合并到代码库前审查 Copilot 智能体模式生成的更改和测试。

## 场景

随着游戏数量增加，你希望允许用户按类别和发行商筛选。前一练习中已添加发布商辅助函数，现在将使用 Copilot 智能体模式完成剩余的数据层、界面和测试工作。

## 运行 Tailspin Toys 网站

进行更改前，先探索 Tailspin Toys 网站，了解其当前功能。

网站是面向以开发者为主题的桌游的众筹平台。用户可以查看游戏列表并查看详情。此网站是一个 Astro应用，构建时将页面渲染为静态 HTML。页面通过 Drizzle ORM直接在 frontmatter中查询本地 SQLite数据库；不存在独立后端 API或客户端 UI框架。可复用的数据访问辅助函数位于 `src/lib/`中，交互通过使用标准 DOM API的少量、限定范围的 Astro `<script>`实现。

### 启动网站

为简化网站运行，本项目提供 `npm run dev`任务，用于启动单个 Astro开发服务器。在 GitHub Codespace中运行：

1. 返回 Codespace。完成上一练习后，应已回到 `main`。
2. 在 Codespace中按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端窗口。
3. 创建并切换到筛选工作的新分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 运行以下命令启动网站：

   ```bash
   npm run dev
   ```

   Astro开发服务器准备就绪后，会看到类似下面的横幅：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果出现提示打开 `http://localhost:4321`浏览器窗口的对话框，请选择 **x**关闭。

5. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），选择终端中的 Astro服务器地址 `http://localhost:4321`打开网站。

> [!NOTE]
> 使用 Codespace时，选择终端中的 localhost链接会自动重定向到 `https://<your-codespace-name>-4321.app.github.dev/`。这是指向正在托管 Web服务器的 Codespace私有隧道！

### 浏览网站

网站运行后，可以探索其功能。主要功能包括：

- **主页**：显示带标题、图片和描述的桌游列表。
- **游戏详情页**：选择游戏后进入详情页，可查看标题、描述、发行商和类别等信息。

## 使用 Copilot 浏览待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始下面练习前，返回 Codespace，打开 Copilot Chat面板，并选择 **New Chat**开始全新对话。

网站初始实现已经可用，但需要增强功能。先审查待办事项。从模板设置项目时，议题待办事项会自动创建；请让 GitHub Copilot展示这些项目。

1. 在 Chat视图的智能体下拉列表中选择 **Agent**。**Agent**智能体会自主规划并实现跨文件更改、运行终端命令并调用工具。

   ![Chat视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本研讨会作者并不表示偏好某个模型。在编写研讨会时使用的是 Claude Sonnet 4.5，因此示例中包含该选择。希望模型建议相对一致，以保证良好体验。但由于大语言模型具有概率性，你看到的建议可能与研讨会说明不同，这是正常且预期的。

> [!NOTE]
> 由于大语言模型具有概率性，Copilot可能使用不同的 MCP命令，但仍应能完成任务。

3. 使用以下提示询问 Copilot 仓库待办事项：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue**运行列出全部议题的命令。
5. 审查生成的议题列表。

注意 Copilot如何根据对用户最有用的议题为其排序。

## 审查指令文件

在启动智能体生成代码前，适合先审查将用于向 Copilot 提供工作上下文的指令文件。你将使用 [UI（用户界面）](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)文件，其中包含为网站添加功能时应遵循的上下文。

1. 在 Codespace中导航到 `.github/instructions/ui.instructions.md`。
2. 注意关于添加功能方法的整体指导，包括：
   - 架构概述。
   - 组件设计、可测试性和无障碍访问原则。
   - 指向 Astro、Tailwind CSS和 Drizzle等不同文件类型的具体指令文件链接。

> [!TIP]
> 指令文件允许引用其他指令文件和项目中的文件。路径相对于指令文件所在位置。这有助于复用，将复杂指令拆分为更易管理的片段，并提供示例和模板。

## 实现筛选功能

要完成筛选，应用至少需要三项更新：

- 在数据层（`src/lib/`）添加或完善剩余筛选逻辑。
- 为筛选行为添加或更新测试。
- 更新游戏列表页并引入筛选界面。

此外，合并前测试必须运行且通过。Copilot 智能体模式可以执行这些任务！

1. 可继续当前 Copilot对话，也可选择 **New Chat**开始新对话。
2. 选择 **Add Context**、**Instructions**，再选择 `ui`指令文件。

   ![选择 UI 指令文件示例截图](../../../_images/ex3-select-instructions-file.png)

3. 确保 Chat视图的智能体下拉列表仍选择 **Agent**。

   ![Chat视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

4. 确保模型仍为 **Claude Sonnet 4.5**。
5. 使用以下提示，让 Copilot根据待办事项中的相关议题实现功能：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot如何先探索项目并定位所需功能的文件。它应找到数据层辅助函数、界面及测试，然后开始修改文件并运行测试。

   ![Copilot探索项目文件的截图](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot可能执行探索项目、修改文件和运行测试等任务。耗时取决于任务和代码库的复杂度。在此过程中，代码编辑器可能出现 **Keep**和 **Undo**按钮。Copilot完成后，所有更改都会有 **Keep**或 **Undo**选项，无需在工作进行时逐一选择。

7. 根据 Copilot的提示，选择 **Continue**运行测试。

   ![Copilot Chat窗格询问用户是否运行测试的对话框截图](../../../_images/ex3-agent-mode-run-tests.png)

8. 过程中可能出现暂停，甚至某些测试失败。这很正常！Copilot会在代码生成和测试之间反复迭代，直到完成任务且未检测到错误。

   ![包含 Copilot智能体模式完整 Chat会话的截图](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 浏览生成的代码，寻找潜在问题。

> [!CAUTION]
> 请记住，审查 Copilot或其他 AI工具生成的代码始终很重要。

10. 返回已运行网站的浏览器，并探索新功能！
11. 确信一切正常且已审查代码后，在 Copilot Chat窗口中选择 **Keep**。

## 总结与后续步骤

恭喜！在本练习中，你探索了如何使用 GitHub Copilot智能体模式为 Tailspin Toys网站添加新能力。你了解了：

- GitHub Copilot智能体模式如何在界面和数据层中实现新功能。
- Copilot智能体模式如何探索项目、识别相关文件并进行协调更改。
- 如何在合并到代码库前审查 Copilot智能体模式生成的更改和测试。

现在，[使用 Playwright MCP服务器测试功能][next-lesson]并为它打开拉取请求。

### 奖励探索练习——实现分页

随着游戏数量增加，需要启用分页。使用本练习学到的技能，请 Copilot更新网站并实现分页。代码注意事项包括：

- 遵循现有最佳实践，包括使用现有指令文件。
- 思考分页的实现方式，决定允许用户选择页面大小，还是硬编码。
- 编写提示时，为 Copilot提供实现所需的指导。
- 可能需要与 GitHub Copilot迭代、要求修改并提供上下文。这是与 Copilot协作的正常流程！

## 资源

- [Copilot 的 Ask、Edit 和 Agent模式：用途与适用场景][choose-mode]
- [VS Code中的 Agent模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
