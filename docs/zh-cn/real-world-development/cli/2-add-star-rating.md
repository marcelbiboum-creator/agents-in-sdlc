---
title: "第 2 课——添加星级评分：一次快速入门"
description: "使用 Copilot CLI 修改游戏卡片，在转发的浏览器中审查，并将其作为第一个拉取请求合并。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

现在你已经安装 Copilot CLI 并尝试了一次对话，接下来可以首次修改项目。保持改动较小：游戏数据中已有星级评分，但首页的游戏卡片尚未显示。你将要求智能体展示评分，审查更改，并将其作为第一个拉取请求合并。

在本课中，你将：

- 在功能分支上开始一次聚焦的 Copilot 对话。
- 请智能体对项目进行小幅更改。
- 使用 `/diff` 审查更改。
- 运行应用并在转发的浏览器中确认更改。
- 打开并合并第一个拉取请求。

## 场景

Tailspin Toys 中的每款游戏都有星级评分，并且已在游戏详情页中显示。不过，首页的游戏卡片只显示标题、类别、发行商和描述。作为热身，你将让智能体在每张卡片上显示现有评分——这是一次简小、自包含的改动，非常适合首个会话。

## 对话的组成

**对话**是你与 Copilot CLI 就某项任务协作的场所。与 Copilot app 不同，普通 CLI 对话使用终端中当前检出的仓库和 Git 分支，不会创建专用工作树。保存对话后可以稍后继续讨论，而文件和分支仍是磁盘上的普通 Git 状态。

对话中会看到三类内容：你的提示与智能体的响应、智能体探索和编辑文件时的工具活动，以及可以使用 `/diff` 棡查的更改。

## 开始对话并请求更改

现在开始新的对话来实现功能。

1. 返回你的 Codespace。
2. 如果终端尚未打开，请按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）。
3. 如果尚未启动 Copilot，请运行以下命令：

   ```bash
   copilot --yolo
   ```

4. 使用斜杠命令 `/new` 并按 <kbd>Enter</kbd>，确保已开始新会话。
5. 使用以下提示请求更改：

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot 会探索项目、定位用于显示游戏详情的文件，并创建必要的代码。你已使用 Copilot CLI 添加了新功能！

## 审查差异

即使改动很小，所有 AI 生成的更改在合并前都值得审查。现在就在 Copilot CLI 中检查更改。

1. 输入 `/diff` 并检查每个已更改的文件。
2. 确认游戏卡片在评分存在时显示数值；当 `starRating` 为 `null` 时显示 `No rating yet`。
3. 确认测试覆盖两种状态。
4. 审查 Copilot 运行的检查结果，并要求它修复所有失败项。
5. 完成审查后，按 <kbd>Esc</kbd>退出差异界面。

> [!NOTE]
> 与其他生成式 AI 工具一样，Copilot 具有概率性而非确定性，因此你的确切代码可能有所不同。应审查行为，而不是期待完全一致的实现。

## 检查更改

当然，我们不应只阅读代码而假设它能正常运行。现在请 Copilot 启动网站，以便在 Codespaces 转发的浏览器中检查更新后的用户界面（UI）。

1. 请 Copilot 启动应用：

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. 当 Codespaces 报告端口 `4321` 可用时，选择 **在浏览器中打开**。
3. 确认游戏卡片显示的是满分五分制的星级评分。
4. 返回 Copilot，并请它停止已启动的服务器：

   ```plaintext
   Stop the development server you started.
   ```

## 打开并合并第一个拉取请求

你已经创建了该功能！现在是时候创建拉取请求（PR），将新代码合并到项目中。

1. 请默认智能体提交更改：

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. 输入 `/pr create`。Copilot CLI 创建 PR 时会推送现有提交，并显示 PR URL。
3. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），选择 Copilot CLI 显示的 URL 来打开 PR。
4. 审查已更改的文件和检查。
5. 准备就绪后，选择 **合并拉取请求**，然后确认合并。
6. 返回 Codespace，并使用 `/exit`退出 Copilot CLI。
7. 更新本地 `main`：

   ```bash
   git checkout main
   git pull
   ```

## 总结与后续步骤

恭喜！你已使用 GitHub Copilot CLI 发布了第一个更改！具体而言，你：

- 在功能分支上开始了一次聚焦的 Copilot 对话。
- 指示智能体修改游戏卡片。
- 使用 `/diff`审查更改。
- 运行应用并在转发的浏览器中确认星级评分。
- 打开并合并了第一个拉取请求。

接下来，你将[从筛选议题入手并使用 Plan 和 Autopilot 模式][next-lesson]构建更大的功能。

## 资源

- [关于 GitHub Copilot CLI][about-copilot-cli]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
