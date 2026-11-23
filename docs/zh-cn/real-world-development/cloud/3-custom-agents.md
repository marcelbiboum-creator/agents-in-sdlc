---
title: "练习 3——自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 中的[自定义智能体][custom-agents-concept]允许你创建专门针对开发工作流中特定任务或领域的 AI助手。通过仓库 `.github/agents`文件夹中的 Markdown 文件定义智能体，可以为 Copilot 提供聚焦指令、最佳实践、编码模式和领域知识，引导它更有效地完成特定类型的工作。团队可以将专长固化为可复用智能体，例如强制遵循 [WCAG][wcag]合规性的无障碍智能体、遵循安全编码实践的安全智能体，或维持一致测试模式的测试智能体。

自定义智能体由项目 `.github/agents`文件夹或全局 `~/.copilot/agents`中的 Markdown 文件定义。每个文件都有至少包含 `name`和 `description`的 YAML frontmatter，后接定义智能体行为、专长和指令的 Markdown 提示。

### 自定义智能体与智能体技能的比较

自定义智能体与[智能体技能][agent-skills-concept]存在一定重叠。两者主要都使用 Markdown 文件，并告诉 AI 如何执行操作。最清晰的区分是：**自定义智能体是执行工作的角色**，而**技能是工具**。

自定义智能体拥有自己的上下文窗口，能够在工作中编排技能（甚至其他智能体）。在本实验中，无障碍自定义智能体会根据无障碍指南审查并更新网站；在此过程中，它可能调用拉取请求工作流技能或运行及管理测试的技能。

> [!NOTE]
> 自定义智能体没有唯一正确的编写方式。与任何 AI应用一样，应通过测试和迭代找到适合环境和场景的方法。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

你将通过自定义智能体探索：

- 自定义智能体如何定义。
- 如何将任务分配给自定义智能体。

## 场景

Tailspin Toys 致力于让平台无论用户的视觉能力或偏好如何，都能无障碍访问。近期用户反馈显示，由于文字与背景的对比度不足，部分用户觉得当前深色主题难以阅读。为解决这一无障碍问题，设计团队要求实现可开关的高对比度模式。

由于无障碍访问至关重要，应尽快实现该功能。接下来将使用自定义智能体生成该功能。

## 审查无障碍自定义智能体

仓库已提供一个无障碍自定义智能体。现在审查其内容，了解它如何引导 Copilot。

返回 Codespace，然后审查无障碍自定义智能体文件：

1. 打开 `.github/agents/accessibility.md`。
2. 注意包含 `name`和 `description`字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体的 `name`和 `description`frontmatter 是必需的。

3. 接着浏览并审查以下部分：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - HTML、CSS 和 JavaScript代码示例。
   - 常见陷阱和错误列表。

## 创建并分配议题

Mission control 是处理环境中所有智能体任务的中央位置。你可以将任务分配给 Copilot 云智能体、监控任务，甚至重定向并提供额外指导。现在先分配一个创建高对比度模式的任务。

1. 导航到仓库。
2. 选择 **Issues**选项卡。
3. 选择 **New issue**打开新议题对话框。
4. 选择 **Blank issue**创建新议题。
5. 将 **Title**设为 `Add high contrast mode to website`。
6. 将 **Description**设为：

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. 选择 **Create**创建议题。
8. 在右侧选择 **Assign to Copilot**打开分配对话框。
9. 从自定义智能体列表中选择 **Accessibility agent**。

    ![云智能体分配界面，高亮显示自定义智能体和 Accessibility](../../../_images/ex5-select-custom-agent.png)

10. 选择 **Assign**。
11. Copilot 会在后台开始处理任务！

## 总结与后续步骤

本课探索了 GitHub Copilot 中的[自定义智能体][custom-agents]，即针对特定任务和领域定制的专用 AI助手。通过自定义智能体，你可以将团队专长和标准固化为可复用智能体，引导 Copilot 更有效地完成特定类型的工作。

你探索了以下概念：

- 自定义智能体如何定义。
- 如何将任务分配给自定义智能体。

Copilot 正在实现高对比度模式，现在可以在 Mission Control中[监控并引导智能体会话][next-lesson]。

## 资源

- [关于自定义智能体][custom-agents]
- [为组织准备使用自定义智能体][org-custom-agents]
- [为企业准备使用自定义智能体][enterprise-custom-agents]

---

| [← 上一课：GitHub Copilot 云智能体][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
