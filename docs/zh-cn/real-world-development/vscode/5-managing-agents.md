---
title: "练习 5——监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义智能体][previous-lesson] |
|:--|

将 GitHub Copilot置于智能体模式后，它会自主探索代码库、提出更改、编辑文件并运行命令。由于工作实时在你的机器上进行，VS Code中的 Copilot Chat会显示智能体进行的每次工具调用和文件编辑。你可以在行内审查每个差异，接受或拒绝单独更改，并使用后续提示引导对话，以在不离开编辑器的情况下优化或扩展工作。

在本练习中，你将：

- 实时监控无障碍智能体的工作。
- 审查并接受建议的文件编辑。
- 在会话进行中引导智能体添加浅色模式切换，与高对比度模式并列。

## 场景

你在[练习 4][previous-lesson]中使用的无障碍自定义智能体正在实现高对比度模式。工作进行中，设计团队提出了额外请求：他们希望添加浅色模式切换，供觉得默认主题过暗的用户使用。无需重新开始对话，你将引导现有会话扩展工作。

## 监控 Copilot的进度

Copilot Chat视图会显示智能体执行的每一步，包括探索的文件、运行的命令和提出的编辑。每项文件编辑都会以内联方式显示在聊天中，并附有差异以及 **Keep** / **Undo**控件。

1. 返回练习 4中的 Copilot Chat视图。
2. 智能体工作时，滚动聊天查看每次工具调用。你会看到读取文件、编辑文件，以及要求运行的终端命令。
3. 智能体提出文件编辑时，差异会以内联方式出现：
    - 选择 **Keep**接受更改。
    - 选择 **Undo**恢复更改，让智能体再试一次。
4. 可打开聊天顶部的 **Files changed**指示器，查看本次会话中智能体修改的完整工作集。

> [!NOTE]
> 如果工具调用请求权限（例如运行终端命令），智能体会暂停并显示 **Allow**提示。只批准你认为安全的命令。

5. 等待智能体完成高对比度模式实现。最终消息应总结它所作的更改。

## 引导智能体添加浅色模式

高对比度模式已就位，现在继续同一个对话以添加浅色模式切换。由于延续同一个聊天会话，智能体会保留此前工作中的上下文，包括它修改过的组件、采用的样式方法以及已设置的 local-storage模式。

1. 在 Copilot Chat输入框中发送以下后续提示：

    ```plaintext
    Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
    ```

2. 智能体将从中断处继续，探索已修改的内容并提出浅色模式的新增部分。
3. 与审查高对比度模式时一样，审查每项新增编辑。对每个差异选择 **Keep**或 **Undo**。
4. 如果智能体朝你不希望的方向发展（例如尝试以不合适的方式重构切换界面），可选择聊天输入框旁的 **Stop**按钮停止它，然后发送澄清后的后续消息。

> [!TIP]
> 引导进行中的会话比重新开始更快。可使用后续提示请求调整（“简化 CSS——使用 CSS变量，不要重复选择器”）、纠正方向（“不要添加第三个切换，将浅色模式集成到现有设置面板”），或扩展范围（“同时为两个切换添加键盘快捷键”）。

## 审查工作集

提交工作前，请快速检查智能体修改的全部内容。

1. 在 VS Code中打开 **Source Control**视图。
2. 审查完整的已更改文件列表。应看到 Astro组件、样式及相关测试的更新。
3. 打开几个已更改的文件并逐项查看差异。确认自定义智能体的无障碍模式已体现，包括 ARIA属性、键盘导航、语义化 HTML以及通过 local storage持久化。
4. 满意后，在 Source Control面板中暂存并提交更改。将在[下一课][next-lesson]发布它们。

## 总结与后续步骤

你使用 Copilot Chat智能体模式监控并引导了进行中的会话：在每项文件编辑落地时审查，接受或拒绝更改，并发送后续提示在不丢失上下文的情况下扩展工作。

在本课中，你探索了：

- 实时监控智能体的工作。
- 接受或拒绝单独的文件编辑。
- 使用后续提示在会话进行中引导智能体。

在[下一课][next-lesson]中，你会将无障碍工作发布为拉取请求，并审查本实验中本地自定义智能体产生的更改。

## 资源

- [VS Code中的 Copilot Chat][copilot-chat-vscode]
- [使用智能体模式][agent-mode]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
