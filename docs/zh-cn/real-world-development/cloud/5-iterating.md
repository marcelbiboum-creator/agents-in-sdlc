---
title: "练习 5：迭代 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作成果

在本实验中，你已与 GitHub Copilot 合作完成多个任务，用于改善用户体验和添加功能。你要求 Copilot 为代码添加文档，为设计团队构建相关游戏功能，并实现包括高对比度和浅色模式切换在内的无障碍功能。现在探索代码更改，并在必要时向 Copilot 提供反馈以改进工作。

### 场景

正如多次强调的，生成式 AI不会改变软件设计和 DevOps 的基本原则。我们始终应审查生成的代码，并遵循常规 DevOps 流程。有鉴于此，在向团队其他成员开放审查前，先审查 GitHub Copilot 为文档、相关游戏功能和无障碍功能提出的建议。

## 安全与 Copilot 云智能体

由于 Copilot 云智能体异步且无人工监督地执行任务，因此设置了特定安全约束以确保一切安全。这些约束包括：

- Copilot 对仓库只有读取权限，仅对用于编写代码的分支具有写权限。
- 云智能体在 GitHub Actions 中运行，并创建独立、临时的工作环境。
- 所有 GitHub Actions 工作流都需人工批准后才能运行。
- 默认限制[对外部资源的访问][agent-firewall]，包括 MCP 服务器。

## 审查生成的文档

先探索 GitHub Copilot 云智能体生成的第一个拉取请求（PR），即为代码添加文档。此任务使用 GitHub.com 上的标准 PR界面完成。

> [!NOTE]
> 浏览 PR 时可能看到 GitHub Copilot 被防火墙阻止的警告。这是**预期行为**，因为 Copilot 默认对外部资源的访问受限，包括外部 MCP服务器调用。如果需要，可为 Copilot 云智能体[自定义或禁用防火墙][agent-firewall]。

1. 返回仓库的 github.com 页面。
2. 选择 **Pull Requests**打开拉取请求列表。
3. 打开标题类似于 **Add missing documentation**或更具体的拉取请求。

> [!NOTE]
> 如果 Copilot仍在处理任务，PR 会包含 **[WIP]**标记。如有，请等待 Copilot 完成。这可能需要几分钟，可以休息或回顾迄今学到的内容。

4. PR准备好后，选择 **Files changed**选项卡并审查更改。

    ![Files changed选项卡](../../../_images/shared-pr-files-changed.png)

5. 浏览新更新的代码，其中包括新增的 TSDoc文档注释和其他文档。具体更改会有所不同。

    浏览更改时，注意 TSDoc文档注释、TypeScript约定和注释标题。这些来自练习 2开始时审查的自定义指令文件。

6. 审查更新并确认无误后，返回 **Conversation**选项卡并向下滚动。
7. 应看到某些工作流正在等待批准的指示。
8. 如果工作流正在等待批准，选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

9. 工作流应进入 PR 检查队列。正常情况下，单一 Astro应用的项目检查会通过。此过程可能需要几分钟。

## 请求 GitHub Copilot 修改

与 PR中的 Copilot 协作不是单向流程。你也可以像标记团队成员一样，在 PR评论或代码行内评论中标记 Copilot。Copilot 会看到这些评论，并启动新会话处理反馈。由于结果具有非确定性，无法提供固定措辞。可请求 Copilot 更新的示例包括：

- 在每个代码文件顶部添加注释标题，简要说明文件用途。
- 为 TypeScript 和 Astro 文件添加 TSDoc文档注释。
- 创建 README，描述 Astro应用结构。

1. 添加请求更改的评论，像标记其他用户一样标记 **@copilot**。可使用上述建议之一，也可提出你希望在代码库中看到的其他文档改进。
2. 选择 **View Session**观看 Copilot执行工作。注意 Copilot 如何启动新会话进行更新。
3. 可选择 **Back to pull request**返回拉取请求。

    ![返回拉取请求](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成更改后，PR 中应出现新的提交。
5. 选择 **Files changed**选项卡审查更改。

可以继续迭代，直到满意为止。满意后，可将 PR 从草稿转换为可审查状态，并合并到 main 分支。

![将 PR 转为可审查状态](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

下面返回 Copilot 为解决游戏详情页显示相关游戏议题而生成的 PR。

1. 返回 GitHub.com 上的仓库。
2. 选择 **Pull Requests**选项卡。
3. 选择标题类似于 **Show related games on the game details page**或更具体的 PR。
4. 选择 **Files changed**选项卡审查生成的代码。
5. 审查更新并确认无误后，返回 **Conversation**选项卡并向下滚动。
6. 应看到某些工作流正在等待批准的指示。
7. 如果工作流正在等待批准，选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

8. 工作流应进入拉取请求的检查队列。正常情况下，单一 Astro应用的项目检查会通过。此过程可能需要几分钟。
9. **可选：**可在 Codespace 中切换到该分支，手动测试相关游戏功能。导航到 Codespace，打开终端，并运行以下命令（将 `<branch-name>`替换为 Copilot 创建的分支名称，例如 **copilot/fix-8**）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot 已构建相关游戏功能！与之前一样，你可以与 Copilot 云智能体迭代并请求更新。例如，可以要求调整显示的相关游戏数量，或确保添加注释标题和 TSDoc文档注释（请记住：分配此任务时，你尚未更新自定义指令！）。与之前一样，可在 **Conversation**选项卡中添加评论提出这些请求，Copilot 会启动新会话。

## 审查无障碍功能

最后，审查使用无障碍自定义智能体实现的无障碍功能。此 PR应同时包含练习 3中分配的高对比度模式，以及练习 4在 Mission Control中请求的浅色模式。

1. 返回 GitHub.com 上的仓库。
2. 选择 **Pull Requests**选项卡。
3. 选择标题类似于 **Add high contrast mode to website**或更具体的 PR。

> [!NOTE]
> 如果 Copilot仍在处理任务，PR 会包含 **[WIP]**标记。如有，请等待 Copilot 完成。这可能需要几分钟。

4. 选择 **Files changed**选项卡审查生成的代码。
5. 审查实现时，特别注意：
   - 用于切换模式的 UI组件。
   - 使用 local storage保存用户偏好。
   - 高对比度模式和浅色模式的 CSS或样式更改。
   - 无障碍属性（ARIA标签、键盘导航等）。
   - 管理模式切换的 JavaScript/TypeScript代码。

6. 审查更新并确认无误后，返回 **Conversation**选项卡并向下滚动。
7. 应看到某些工作流正在等待批准的指示。
8. 如果工作流正在等待批准，选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

9. 工作流应进入拉取请求的检查队列。正常情况下，单一 Astro应用的项目检查会通过。此过程可能需要几分钟。
10. **可选：**可切换到 Codespace中的该分支，手动测试无障碍功能。导航到 Codespace，打开终端，并运行以下命令（将 `<branch-name>`替换为 Copilot 创建的分支名称）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    然后启动应用，在浏览器中测试高对比度和浅色模式切换，确保它们按预期工作，并在页面重新加载后仍然保留。

注意自定义无障碍智能体如何引导 Copilot 按无障碍最佳实践实现这些功能。如果发现无障碍问题或改进建议，可像处理前面的 PR一样，在评论中标记 **@copilot**请求更新。

## 可选练习——继续委派

当你能够将真实待办事项交给云智能体并专注于其他工作时，云智能体效果最佳。为养成这一习惯，可再向仓库提交几个议题并分配给 Copilot。一些想法：

- 在游戏详情页创建支持者兴趣表单。
- 在游戏列表页实现分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

你已完成 Cloud agent流程。在这些课程中，你：

- **检查了此仓库附带的自定义指令文件**，以便稍后观察它们对云智能体输出的影响。
- **将议题分配给 Copilot 云智能体**，并观察它设置环境、制定计划并异步执行。
- **创建并使用无障碍自定义智能体**，添加高对比度和浅色模式切换。
- **使用 Copilot 智能体页面作为 Mission Control**监控并在会话运行期间引导无障碍会话。
- **审查并迭代云智能体的拉取请求**，标记 `@copilot`请求更改并批准工作流。

## 审查与后续步骤

你已完成 Cloud agent流程。如果希望继续探索，其他流程可补充此处练习：

- 🖥️ **[VS Code 流程](../../vscode/)**——直接在 IDE 中探索 Copilot Chat 智能体模式和 MCP集成。
- 💻 **[CLI 流程](../../cli/)**——在终端中交付两个经过审查的更改，使用 Plan 和 Autopilot 模式、智能体技能、自定义 QA智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate`通往云智能体的桥梁。

在自己的仓库中，可尝试以下后续想法：

- 将重构或测试覆盖率议题分配给云智能体。
- 为其他领域创建自定义智能体。
- 为其他技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
