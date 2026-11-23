---
title: "第 3 课——智能体模式：Plan 和 Autopilot"
description: "使用 Plan 达成方案共识，使用 Autopilot 根据议题构建筛选功能，并使用交互模式审查结果。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

我们已经在项目中添加了一个小功能，但较大的更改需要更完善的流程。幸运的是，GitHub Copilot CLI 可以融入组织现有的工作流，确保我们正确地构建所需内容。本课是后续多个课程中的第一课，你将遵循典型的智能体驱动开发流程：先使用议题生成新功能，再确保代码有效、功能符合预期，最终成功合并。

> [!NOTE]
> 在贯穿整个功能工作流时，你将使用同一个对话和分支。通常，处理不同类型的文件时应使用不同分支或 PR，但这里会采用一种简化方式，以便集中关注核心概念。

在本课中，你将：

- 从 GitHub议题启动新的 Copilot 对话。
- 在 Plan 模式中定义需求。
- 使用 Autopilot 模式实现新功能。
- 审查代码。
- 在转发的浏览器中手动验证功能。

继续实现该功能时，你将更新仓库指令、自定义现有的 `quality-checks` 技能、添加 MCP 验证、创建 QA 智能体，并打开功能 PR。

## 场景

Tailspin Toys 的目录不断增长，访问者需要按类别和发行商筛选游戏。待办事项议题描述了该功能，但组合类别等细节需要在编码前达成一致。你将使用 Plan 模式解决这些决策，然后通过 Autopilot 授权进行有界实现。

## 背景

将 AI 编码智能体引入开发流程不会改变基本原则；如果说有影响，那就是这些原则更加重要！大多数开发人员遵循类似流程：

1. 从描述待办工作的议题开始。
2. 制定需要构建的计划。
3. 构建并审查代码。
4. 运行测试以验证代码。
5. 手动验证新功能。
6. 创建拉取请求（PR）。
7. 在代码审查完成且持续集成成功后合并代码。

> [!NOTE]
> 具体操作会因团队和组织而异，但多数流程都与上述主题类似。

坚持这种标准方法，可以确保 AI 生成的代码符合需求，并通过与手写代码相同的审查流程。

## 对话模式

**对话模式**控制智能体的自主程度。按 <kbd>Shift</kbd>+<kbd>Tab</kbd>循环切换模式：

- **Interactive**：你与智能体协作。智能体提出更改，并在继续之前等待你的输入。
- **Plan**：智能体先制定计划，不允许编辑项目文件。
- **Autopilot**：智能体自主工作，包括编写代码、运行测试并迭代，直到完成任务。

先进入 Plan 模式、审查计划，然后使用 Autopilot 实现。

## 从议题开始

开始筛选工作前，请返回 Codespace，并确保仓库和终端已准备就绪。

1. 返回 Codespace。如果它已停止，请先重启再继续。
2. 确认星级评分 PR 已合并。
3. 如果终端尚未打开，请按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）。
4. 更新 `main`，然后为筛选工作创建分支：

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. 启动 Copilot CLI：

   ```bash
   copilot --yolo
   ```

6. 连按两次 <kbd>Tab</kbd>打开 **Issues** 选项卡。
7. 按 <kbd>A</kbd>显示全部议题。
8. 使用方向键选择标题为 **Allow users to filter games by category and publisher** 的议题。
9. 按 <kbd>C</kbd>将议题添加到提示中并返回 **Session** 选项卡。

注意提示现在以 `#7`（或类似编号）开头。使用 `#` 可以将 GitHub 上的议题或拉取请求（PR）引入上下文。

## 规划筛选功能

规划让你有机会先定义实现功能或执行任务的方法，再交给 Copilot。对于复杂工作，花一点时间规划通常是好主意。现在切换到计划模式，请 Copilot 创建计划。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd>切换到 Plan 模式。确认提示下方的模式指示器显示 **Plan**。
2. 在前一步添加的议题引用之后，输入以下提示：

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot 开始制定计划！它会先探索项目，再确定最佳方法。

3. 过程中，Copilot 可能会询问筛选功能应如何工作。请根据你的偏好回答。这里没有唯一正确答案！
4. 计划完成后，按 <kbd>Control</kbd>+<kbd>E</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>E</kbd>（Windows/Linux）展开计划。
5. 上下滚动以审查计划。
6. 如果计划的任何部分与你的决定不符，请请 Copilot 修改。

## 批准 Autopilot

计划已经编写并审查完毕，现在可以实现它了！让 Copilot 使用 autopilot 完成工作。

Autopilot 会迭代解决问题，直到它认为任务已经完成。

1. 选择 **Accept plan and build on autopilot (recommended)**，或已安装版本中标签相似的选项。
2. 确认提示下方的模式指示器显示 **Autopilot**。
3. 观察 Copilot 按既定计划迭代、生成代码并运行测试。

> [!NOTE]
> 批准可能会立即开始实现，因此请先审查计划。如果 Copilot 报告缺少依赖项或端口冲突，请先解决设置问题，再将检查视为完成。

## 审查并验证实现

代码生成后，需要像审查其他代码一样审查后再合并。下面同时审查代码并运行网站，确保一切正常。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd>进入 Interactive 模式。确认模式指示器不再显示 **Plan** 或 **Autopilot**。
2. 输入 `/diff`并检查筛选实现及测试。
3. 将结果与议题以及规划期间作出的决定进行比较。
4. 完成代码审查后，按 <kbd>Esc</kbd>退出差异视图。
5. 审查项目检查的输出，并请 Copilot 解决所有失败项。

## 探索新功能

代码看起来没问题，但能否运行？让我们像之前一样启动应用，并通过 Codespaces 转发的端口打开网站。

1. 请 Copilot 启动应用：

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. 当 Codespaces 报告端口 `4321` 可用时，选择 **在浏览器中打开**。
3. 尝试类别筛选、发行商筛选，以及你在计划中约定的组合筛选。
4. 确认重置和无结果行为与议题及你的决定一致。
5. 返回 Codespace，并请 Copilot 停止它启动的开发服务器。

## 总结与后续步骤

你已使用不同的对话模式构建并审查功能。在本课中，你：

- 从 GitHub议题启动了新的 Copilot 对话。
- 在 Plan 模式中定义了需求。
- 使用 Autopilot 模式实现了新功能。
- 审查了代码。
- 在转发的浏览器中手动验证了功能。

接下来，我们将进一步了解代码如何生成，以及如何确保代码遵循文档化实践：[使用自定义指令][next-lesson]。

## 资源

- [GitHub Copilot CLI 中的 Autopilot][autopilot]
- [Copilot CLI 命令参考][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
