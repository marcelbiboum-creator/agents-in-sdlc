---
title: "第 10 课——总结与后续步骤"
description: "回顾 Copilot CLI 工作流、两个拉取请求、可复用自定义设置及更多资源。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

你已在连续的 Tailspin Toys 工作流中使用 GitHub Copilot CLI。你：

- 准备了 Codespace，安装了 Copilot CLI，探索了项目，并找到了预置的筛选议题。
- 添加了星级评分，在转发的浏览器中审查结果，并手动合并了第一个拉取请求（PR）。
- 从筛选议题开始，在 Plan 模式中定义方案，在 Autopilot 模式中构建功能，并在 Interactive 模式中审查。
- 使用自定义指令引导智能体，自定义现有的 `quality-checks` 技能，并用它运行单元测试、lint 和类型检查。
- 添加了 Playwright 模型上下文协议（MCP）服务器，并用它在真实浏览器中探索筛选功能。
- 创建并选择了质量保证（QA）自定义智能体，以评估需求、覆盖率、技能结果和浏览器证据。
- 审查了完整筛选更改，并为筛选 PR 授权 Agent Merge。
- 探索了用于上下文、模型、共享和可选云委派的斜杠命令。

## 交付成果

研讨会包含两个 PR里程碑，每个里程碑都基于更新后的 `main` 位于独立分支：

1. **星级评分：**在游戏卡片上显示现有的 `starRating`和明确的未评分状态。
2. **筛选和质量工作流：**实现筛选、更新并应用指令到功能、自定义 `quality-checks`报告、创建 QA 配置并包含相关测试。

从规划筛选到打开其 PR，你始终使用同一个对话和分支。为简化研讨会，我们将这些工作合并到一个 PR 中。

## 不同类型的验证

你通过多种方式检查代码：自动化测试、自己的浏览器检查，以及 Copilot通过 MCP进行的浏览器探索。`quality-checks` 技能运行了单元测试、lint 和类型检查，并以新格式报告。QA 在打开 PR 前将这些结果与需求审查和测试覆盖率审查结合起来。

新增测试应弥补真实空缺；无需新增测试且运行结果良好的 QA 过程同样可能是正确的。授权合并前，请审查代码和证据，并在更改后刷新受影响的证据。

## 最佳实践

提供给 Copilot 的上下文和工具会影响其工作。在本研讨会中，你更新了指令、自定义了技能、创建了 QA 配置，并配置了 MCP 服务器。在不同对话中复用这些自定义设置，并随团队需求变化进行调整。指令设定标准，技能描述可重复任务，自定义智能体定义专用角色，MCP 服务器连接外部工具。审查实际更改和工具结果，不要只看智能体摘要。

让**模式和模型**匹配任务。使用 **Plan**在构建前思考方案，使用 **Interactive**在聚焦的更改中保持参与，使用 **Autopilot**处理范围明确的任务。常规编辑可选择更快的模型，复杂工作可选择能力更强的模型。

上下文仍然和基础设施同样重要。清楚说明希望构建的内容、原因以及实现方式，会显著影响输出。

## 更多可探索内容

你已学习核心工作流。下面是值得继续了解的更多 CLI 功能：

- `/review`：请代码审查智能体分析更改。
- `/rubber-duck`：讨论问题并获得其他视角。
- `/fleet`：并行协调独立子任务。
- `/worktree`：隔离独立任务。
- `/delegate`：将任务发送给 Copilot 云智能体。

## 后续步骤

提升工具使用能力的最佳方法就是持续使用！用它处理生产代码、业余项目，以及你考虑多年却一直没时间构建的小应用。与团队分享经验，也向团队成员学习。并且像往常一样，继续探索文档。

如果想从终端扩展 Tailspin Toys，请继续学习可选的 [Foundry 礼宾服务系列][foundry]。要比较其他环境，请探索 [VS Code 研讨会][vscode]、[GitHub Copilot app 研讨会][app]或 [Copilot 云智能体研讨会][cloud]。

## 资源

- [关于 GitHub Copilot CLI][about-cli]
- [Copilot CLI 命令参考][cli-reference]
- [自定义 Copilot CLI][customize-cli]
- [使用 Copilot CLI 管理拉取请求][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
