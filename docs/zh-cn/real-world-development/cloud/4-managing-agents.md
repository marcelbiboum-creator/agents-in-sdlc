---
title: "练习 4——监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在前几个练习中，你要求 Copilot 云智能体承担三项不同任务，目标是改善用户体验并添加功能。虽然云智能体设计为异步、自主运行，但监控这些任务仍然很重要。

GitHub.com 上的[智能体页面][agents-page]等工具可用于管理分配给云智能体的任务。在这个 Mission Control 中，你可以看到所有具有开放拉取请求（PR）的智能体任务，并查看操作过程，甚至引导正在进行的会话。

在本课中，你将：

- 浏览智能体页面以监控云智能体任务。
- 引导正在运行的会话以请求其他功能。

## 场景

分配智能体创建高对比度模式后，团队认为也应添加浅色模式。既然已经在更新网站样式并添加切换功能，顺便加入此功能是合乎逻辑的。你希望引导智能体的工作，使其同时添加浅色模式和高对比度模式。

## 审查 Copilot 云智能体任务

下面查看分配给 Copilot 云智能体的所有任务当前状态。

1. 导航到 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 注意主窗格和左侧窗格中的任务列表。你应看到已分配给 Copilot 的任务，包括：
    - 更新代码库文档。
    - 生成用于修改游戏的 API。
    - 为网站添加高对比度模式。
3. 选择一个正在运行的任务。审查 Copilot 已执行的任务。这些可能包括：
    - 从仓库检出代码。
    - 为 Copilot 创建环境。
    - 设置 MCP服务器。
    - 执行分配任务所需的各种步骤。

> [!NOTE]
> 列出的具体步骤会因 Copilot 工作状态和采用的方法而有所不同。

4. 注意右侧出现的拉取请求（PR）窗格。它允许你查看 PR 和已更改的文件，以便进一步监控。

## 引导云智能体

既然已看到活动任务，现在请求 Copilot 在处理高对比度模式的同时添加浅色模式切换。

1. 选择与添加高对比度模式相关的会话。具体标题可能因 Copilot 使用的名称和当前工作状态而异。

    ![Mission Control中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到它显示已完成设置并开始工作。看到类似以下的消息时，即表示已开始：
3. 在 **Steer active session while Copilot is working**对话框中添加以下提示：

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![智能体页面中的云智能体任务，突出显示 steer active session while Copilot is working 对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd>发送提示。
5. 注意 Copilot 如何确认提示并将它纳入工作流程。

## 让 Copilot 完成工作

与之前一样，Copilot 将开始处理更新后的任务！发送消息后，它会在完成当前步骤后将新请求纳入流程。

与之前一样，此过程可能需要几分钟；现在正好可以暂停并回顾迄今学到和探索的内容。

## 总结与后续步骤

本课探索了 Copilot 智能体页面，即监控和引导 GitHub Copilot 云智能体任务的中央中心。通过这个 Mission Control，你可以跟踪所有活动和已完成任务、审查正在执行的工作，甚至重定向进行中的任务以调整范围或提供更多指导。

你探索了以下概念：

- 使用 Mission Control和智能体页面监控云智能体任务。
- 重定向正在运行的会话以请求其他功能。

Copilot 正在完成无障碍功能，现在可以转向[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
