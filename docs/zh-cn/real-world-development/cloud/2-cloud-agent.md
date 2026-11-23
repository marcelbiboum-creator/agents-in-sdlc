---
title: "练习 2——GitHub Copilot 云智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义指令][previous-lesson] |
|:--|

几乎没有组织不为技术债而头疼。这可能是未解决的安全问题、需要更新的旧代码，也可能是因没有时间实现而长期留在待办事项中的功能请求。GitHub Copilot 云智能体可以自主更新代码、添加功能等。智能体完成工作后，会生成供人类开发人员审查的草稿 PR。这样可以卸载繁琐任务、加速开发过程，并让开发人员专注于更宏观的工作。

你将通过 Copilot 云智能体探索：

- 自定义代码生成环境。
- 确保操作安全执行。
- 明确限定议题范围的重要性。
- 将议题分配给 Copilot。

## 场景

Tailspin Toys 希望处理一些技术债。最初为网站创建首个版本的承包商留下了不理想的文档——更准确地说，几乎完全没有文档。作为第一步，团队希望为应用中所有导出的函数添加 TSDoc 文档注释。

此外，设计团队希望改进游戏发现体验。他们希望每款游戏的详情页都显示相关游戏，即同类别中的其他游戏，方便用户继续浏览。团队暂时不需要完善实现，只需要可用于验收测试用户体验的内容。这是一项当前阻塞项，但还有更高优先级的议题。

这两项任务都很容易被延后，正适合分配给 Copilot 云智能体。Copilot 云智能体会异步处理任务，让开发人员专注于其他工作，稍后再审查 Copilot 的成果并确认一切符合预期。

## Copilot 云智能体简介

[GitHub Copilot 云智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent)可以在后台执行任务，方式与人类开发人员类似。与人类协作一样，它支持多种处理方式，包括[将 GitHub议题分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)。分配后，Copilot 会创建草稿拉取请求用于跟踪进度、设置环境并开始工作。任务进行中或完成后，你都可以查看 Copilot 的会话。方案准备好供你审查时，Copilot 会在拉取请求中标记你。

## 明确定义任务范围的重要性

GitHub Copilot 并无魔法，也不能省去思考。即使看似简单的操作，在深入研究后也可能包含复杂度，因此请[注意如何为 Copilot 云智能体限定任务范围][cloud-agent-best-practices]。把它当作 AI结对程序员：分阶段工作、学习、实验，并根据进展调整。添加生成式 AI 不会改变软件开发的基本原则。

## 当前仓库中的自定义指令

前面的练习介绍了自定义指令及其如何引导 Copilot。如果你已完成自定义指令实操，可以看到 `.github/copilot-instructions.md`的作用；如果尚未完成，现在正是快速查看的好时机。在将工作分配给 Copilot 云智能体前，请只读查看仓库中已有的指令文件，以便稍后观察效果。

在仓库的 GitHub 网页界面或正在运行的 Codespace 中打开以下文件：

- `.github/copilot-instructions.md`——审查 **Code standards**部分，尤其是 TypeScript 和 TSDoc 文档注释的要求。
- `.github/instructions/unit-tests.instructions.md`——注意 `applyTo` frontmatter，它将这些指令限定到 `**/*.test.ts`文件。

下一节将 `Code lacks documentation`议题分配给云智能体时，请留意生成的拉取请求中的 TSDoc 文档注释、TypeScript约定和注释标题；这些来自上述指令文件。后续审查 PR 时会再次说明。

## 为 Copilot 云智能体设置开发环境

无论参与者是谁，创建代码通常都需要特定环境并运行一些设置脚本，以确保环境处于良好状态。将任务分配给以类似软件工程师方式工作的 Copilot 时也是如此。

云智能体处理工作时使用 [GitHub Actions][github-actions]环境。你可以通过创建[特殊设置工作流][setup-workflow]来自定义该环境，该工作流位于 `.github/workflows/copilot-setup-steps.yml`，会在智能体开始工作前运行。这样智能体就能访问所需的开发工具和依赖项。实验环境已预先配置，以保障研讨会流程和学习体验。它确保 Copilot 能访问 Node.js、项目依赖、端到端测试所需的浏览器二进制文件，以及用于单一 Astro应用的迁移和种子 SQLite 数据库：

```yaml
name: "Copilot Setup Steps"

# 允许从仓库的“Actions”选项卡测试设置步骤
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 将权限设为执行各步骤所需的最低级别。Copilot 将获得自己的令牌。
    permissions:
      # 如果设置步骤中需要克隆仓库（例如安装依赖项），请使用 `contents: read` 权限。如果设置步骤不克隆仓库，Copilot 会在步骤完成后自动克隆。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # 前端 / app 设置 - Node.js（整个应用现为 Astro + Drizzle/libSQL）
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # 迁移并填充本地 SQLite 数据库，以便构建和测试拥有数据。
      - name: Set up the database
        run: npm run db:setup
```

它看起来与其他 GitHub 工作流文件相同，但有几个关键点：

- 它包含一个名为 `copilot-setup-steps`的作业。Copilot 开始处理拉取请求前，该作业会先在 GitHub Actions 中执行。
- 注意 `workflow_dispatch`触发器。它允许你从仓库的 **Actions**选项卡手动运行工作流，因此可以先测试工作流是否成功，而无需等待 Copilot运行。

## 添加文档

虽然每个人都理解文档的重要性，但多数项目要么信息过时，要么完全缺失。这类技术债常常无人处理，会降低生产力、增加维护代码库的难度，也会让新开发者更难加入团队。幸运的是，Copilot 擅长创建文档，这是一个非常适合分配给 Copilot 云智能体的议题。它会在后台生成所需文档，稍后你将在另一练习中审查成果。

1. 在新的浏览器标签页中打开 github.com 上的仓库。
2. 选择 **Issues**选项卡。
3. 选择 **New issue**打开新议题对话框。
4. 选择 **Blank issue**创建空白议题。
5. 将 **Title**设为 `Code lacks documentation`。
6. 将 **Description**设为：

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. 选择 **Create**创建议题。
8. 在右侧选择 **Assign to Copilot**打开分配对话框。

  ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

  ![Copilot 分配详情](../../../_images/ex4-assign-copilot-details.png)

10. 选择 **Pull Requests**选项卡。
11. 打开新生成的拉取请求（PR），标题可能类似于 `[WIP]: Code lacks documentation`。如果列表中还没有新 PR，请稍等片刻并刷新浏览器。
12. 几分钟后，你应看到 Copilot 已创建待办事项列表。

> [!NOTE]
> Copilot 的待办事项列表可能需要几分钟才会出现在 PR 中。Copilot 正在创建环境（运行前述工作流）、分析项目，并确定解决问题的最佳方法。

13. 审查列表及它将完成的任务。
14. 向下滚动拉取请求时间线，应会看到 Copilot 已开始处理议题的更新。
15. 选择 **View session**按钮。

  ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 可能需要刷新窗口才能看到更新后的指示器。

16. 注意你可以滚动查看实时会话，以及 Copilot 如何解决问题，包括探索代码、理解状态、暂停思考并决定合适的计划，以及创建代码。

此过程可能需要几分钟。Copilot 云智能体的主要目标之一是异步执行任务，让你专注于其他工作。接下来将利用这一特性：为 Copilot 云智能体分配另一项任务，同时继续编写代码，为应用添加功能。

## 将相关游戏区域添加到游戏详情页

如前所述，GitHub Copilot 云智能体的一大优势是可以分担工作：你专注于一组任务时，它可以专注于另一组任务。为设计团队添加相关游戏区域可能并不耗时，但节省的时间可用于其他任务。现在将它分配给 Copilot 云智能体！

1. 返回 github.com 上的仓库。
2. 选择 **Issues**选项卡。
3. 选择 **New issue**打开新议题对话框。
4. 选择 **Blank issue**使用空白模板。
5. 将 **Title**设为 `Show related games on the game details page`。
6. 将 **Description**设为：

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. 选择 **Create**创建议题。
8. 在右侧选择 **Assign to Copilot**打开分配对话框。

  ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

片刻之后，你应看到议题首条评论中出现一组 👀，表示 Copilot 正在工作！

![Copilot 使用眼睛表情表示正在处理议题](../../../_images/ex4-issue-eyes-emoji.png)

Copilot 正在认真处理你的第二个请求！Copilot 云智能体的工作方式与软件工程师相似，你无需持续监控，而是在完成后审查即可。现在转向创建和使用自定义智能体。

## 总结与后续步骤

本课探索了 [GitHub Copilot 云智能体][copilot-agents]。通过云智能体，你可以将议题异步分配给 Copilot。你可以用它处理技术债、创建新功能或迁移代码框架。

你探索了以下概念：

- 自定义代码生成环境。
- 确保操作安全执行。
- 明确限定议题范围的重要性。
- 将议题分配给 Copilot。

云智能体正在后台努力工作，现在可以转向创建和使用自定义智能体。[Copilot 云智能体也可以使用 MCP服务器][cloud-agent-mcp]，并可使用前面模块中探索过的自定义指令。

## 资源

- [关于 Copilot 云智能体][copilot-agents]
- [将 GitHub议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
