---
title: "练习 4——自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 中的[自定义智能体][custom-agents-concept]允许你创建专门针对开发工作流中特定任务或领域的 AI助手。通过仓库 `.github/agents`文件夹中的 Markdown 文件定义智能体，可以为 Copilot提供聚焦指令、最佳实践、编码模式和领域知识，引导它更有效地完成特定类型的工作。团队可以将专长固化为可复用智能体，例如强制遵循 [WCAG][wcag]合规性的无障碍智能体、遵循安全编码实践的安全智能体，或维持一致测试模式的测试智能体。

自定义智能体由项目 `.github/agents`文件夹或全局 `~/.copilot/agents`中的 Markdown 文件定义。每个文件都有至少包含 `name`和 `description`的 YAML frontmatter，后接定义智能体行为、专长和指令的 Markdown提示。

### 自定义智能体与智能体技能的比较

自定义智能体与[智能体技能][agent-skills-concept]存在一定重叠。两者主要都使用 Markdown文件，并告诉 AI如何执行操作。最清晰的区分是：**自定义智能体是执行工作的角色**，而**技能是工具**。

自定义智能体拥有自己的上下文窗口，能够在工作中编排技能（甚至其他智能体）。在本实验中，无障碍自定义智能体会根据无障碍指南审查并更新网站；在此过程中，它可能调用拉取请求工作流技能或运行及管理测试的技能。

> [!NOTE]
> 自定义智能体没有唯一正确的编写方式。与其他 AI应用一样，应通过测试和迭代找到适合环境和场景的方法。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## 场景

Tailspin Toys 致力于让平台无论用户的视觉能力或偏好如何，都能无障碍访问。近期用户反馈显示，由于文字与背景的对比度不足，部分用户觉得当前深色主题难以阅读。为解决这一无障碍问题，设计团队要求实现可开关的高对比度模式。

由于无障碍访问至关重要，应尽快实现该功能。接下来将使用自定义智能体生成该功能。

在本练习中，你将：

- 审查现有无障碍自定义智能体。
- 在 Copilot Chat中使用无障碍智能体实现高对比度模式。

## 审查无障碍自定义智能体

仓库已提供一个无障碍自定义智能体。现在审查其内容，了解它如何引导 Copilot。

返回 Codespace，打开终端，并从 `main`创建一个全新的分支用于无障碍工作（将练习 3中的筛选 PR保持独立）：

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. 打开 `.github/agents/accessibility.md`。
2. 注意包含 `name`和 `description`字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体的 `name`和 `description`frontmatter 是必需的。

3. 浏览并审查以下部分：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - HTML、CSS 和 JavaScript代码示例。
   - 常见陷阱和错误列表。

## 在 Copilot Chat中使用自定义智能体

VS Code会在 Copilot Chat视图底部的智能体下拉列表中列出 `.github/agents`中定义的每个自定义智能体。你可以选择一个自定义智能体，将聊天会话限定到该智能体的指令和工具。

> [!TIP]
> **打开 Copilot Chat**
>
> 开始下面练习前，返回 Codespace，打开 Copilot Chat面板，并选择 **New Chat**开始全新对话。

1. 如果尚未选择智能体，请在 Chat视图的智能体下拉列表中选择 **Agent**。

   ![Chat视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

2. 选择聊天视图底部的智能体下拉列表（其中显示当前智能体；默认是 **default**）。
3. 从可用智能体列表中选择 **Accessibility agent**。
4. 向无障碍智能体发送以下提示：

    ```plaintext
    Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
    ```

5. Copilot Chat开始工作：探索代码库、提出更改并应用到项目文件。每项编辑都会以内联方式显示在聊天中，并附带文件路径和差异供审查。
6. 编辑落地时，**Files changed**指示器会更新，以便查看智能体修改的完整工作集。

> [!NOTE]
> 此过程可能需要几分钟。Copilot正在对仓库进行真实修改；工作时会编辑现有文件，例如 Astro组件、CSS和相关测试。

下一练习将审查并引导此进行中的工作。

## 总结与后续步骤

本课探索了 GitHub Copilot中的[自定义智能体][custom-agents]，即针对特定任务和领域定制的专用 AI助手。通过自定义智能体，你可以将团队专长和标准固化为可复用智能体，引导 Copilot更有效地完成特定类型的工作。

你探索了以下概念：

- 自定义智能体如何定义。
- 如何在 Copilot Chat智能体模式中使用自定义智能体。

接下来，你将[监控并引导智能体的工作][next-lesson]：审查实时更改，并为同一会话添加浅色模式切换。

## 资源

- [关于自定义智能体][custom-agents]
- [在 IDE中创建自定义智能体][creating-custom-agents-ide]
- [VS Code中的自定义智能体][custom-agents-vscode]
- [自定义智能体配置][custom-agents-config]
- [awesome-copilot上的自定义智能体][awesome-copilot-agents]

---

| [← 上一课：使用 Playwright MCP服务器测试功能][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
