---
title: "第 4 课——使用自定义指令引导 Copilot"
description: "探索仓库指令，添加文档规范，并将其应用于筛选代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

与生成式 AI 协作时，上下文至关重要。如果某项任务需要特定方式完成，就应让 Copilot 能够获取这些指导。[指令文件][instruction-files]不仅描述希望编写的代码，还说明代码应如何组织。现在筛选功能已经实现，你将探索 Copilot 使用的指令、添加文档规范，并将其应用于代码。

在本课中，你将：

- 探索仓库指令和按路径限定的指令文件如何传递给智能体。
- 更新指令文件，确保遵循编码标准。
- 查看指令文件对代码的影响。

## 场景

作为优秀的开发团队，Tailspin Toys 为开发实践制定了一套规范，其中包括：

- 注释应说明意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 记录用途、参数和返回值；存在可注入的 `db` 参数时也应包含。
- 可复用的 Astro 组件应记录其 `Props` 契约；相关代码变化时，注释应保持同步。
- 保留现有的格式和 lint 指导。

通过指令文件，你可以确保 Copilot 获得符合上述实践所需的信息。

## 指令文件

自定义指令允许你向 Copilot 提供上下文和偏好，帮助它理解你的编码风格和需求。这项强大功能可帮助你引导 Copilot 得出更相关的建议和代码片段。你可以指定首选的编码约定、库，以及希望包含的注释类型。指令既可用于整个仓库，也可按任务上下文用于特定类型的文件。

指令文件分为两类：

- `.github/copilot-instructions.md`：仓库级单个指令文件，会随仓库中的每次请求发送给 Copilot，应包含适用于大多数请求的项目信息。
- `.github/instructions/*.instructions.md`：针对特定语言、文件类型或任务提供指导。

> [!NOTE]
> 不同环境支持的指令格式和能力可能不同。依赖特定格式前，请查阅[自定义指令支持参考][custom-instructions-support]。

## 探索此项目中的自定义指令文件

为了帮助开始，starter 项目中已包含一组指令文件。在进行更改之前，先探索现有内容并观察其影响。

1. 返回 Codespace。
2. 在 Codespace 编辑器中（不是终端）打开 `.github/copilot-instructions.md`。
3. 浏览该文件，注意项目的简要描述和编码指导。这些指令适用于此仓库中与 Copilot 的每次交互。
4. 打开 `.github/instructions` 文件夹并浏览其中的文件。注意其中包含 Astro 文件、Drizzle 数据层、测试等方面的指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`。注意顶部的 `applyTo` 字段，它设置的 glob 决定指令适用于哪些文件。
6. 打开 `.github/instructions/drizzle.instructions.md`，注意它引用了其他指令文件和现有项目文件。这样可以将大型指令集拆分为更小、可复用的文件，并让 Copilot 参考具体示例。

## 更新指令文件以符合团队指导

现有文件是良好起点，但仍有缺口。修改核心 `copilot-instructions.md`，确保新生成的 TypeScript 包含 TSDoc 注释。

1. 在 `.github/copilot-instructions.md`中找到标题为 **Code formatting guidance** 的部分，该部分约位于第 35 行。
2. 将以下内容作为最后一个项目符号添加：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

该文件会自动保存！

## 使用更新后的指导

Copilot CLI 在对话开始时加载仓库指令。保存更新后的指令后，退出并恢复筛选对话，让 Copilot 使用新指导，同时保留功能上下文。

1. 如果筛选对话仍处于打开状态，输入 `/exit`关闭。
2. 在 `game-filters-cli` 分支的仓库根目录恢复已保存的对话：

   ```bash
   copilot --resume
   ```

   如果出现提示，请选择筛选对话并确认已检出 `game-filters-cli` 分支。
3. 请 Copilot 应用更新后的指导：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. 输入 `/diff`并阅读已更改的 TypeScript 文件。注意新生成的 TSDoc 注释，并确认其准确说明代码。

## 总结与后续步骤

你已探索 Copilot CLI 如何从指令文件获取上下文，并将新标准应用于功能。具体而言，你：

- 探索了仓库指令和按路径限定的指令文件如何传递给智能体。
- 更新了指令文件以确保遵循编码标准。
- 观察了指令文件对代码的影响。

接下来，你将[自定义并运行可复用的 quality-checks 技能][next-lesson]，确保持续运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [Awesome Copilot——指令文件及其他资源集合][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
