---
title: "练习 1——自定义指令（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson]

与生成式 AI 协作时，上下文至关重要。如果任务需要特定方式完成，或 Copilot 应了解某些背景信息，就应确保这些上下文可被获取。[指令文件][instruction-files]正是提供此类指导的方式，让 Copilot 不仅知道要做什么，还知道如何做。

在本练习中，你将：

- 探索项目上下文、编码规范和文档标准如何通过仓库自定义指令及按路径限定的指令文件传递给 Copilot。
- 在 `.github/copilot-instructions.md`中添加新的仓库级标准。

> [!NOTE]
> 与 VS Code 和 CLI 流程不同，本练习不需要在此运行前后对比提示，因为 Copilot 云智能体在 GitHub议题上异步工作，实时并排展示影响会比较困难。后续审查云智能体生成的拉取请求时，将能看到指令文件的影响。

## 指令文件

### 场景

作为优秀的开发团队，Tailspin Toys 为开发实践制定了一套规范，其中包括：

- 数据层始终需要单元测试。
- 界面应采用深色模式并呈现现代感。
- 应以 TSDoc 文档注释形式为代码添加文档。
- 应在每个文件顶部添加注释块，说明文件用途。

通过指令文件，你可以确保 Copilot 获得符合上述实践所需的信息。

### 自定义指令

自定义指令允许你向 Copilot 提供上下文和偏好，使它更好地理解你的编码风格和需求。这项强大功能可以帮助你引导 Copilot 提供更相关的建议和代码片段。你可以指定首选编码约定、库，以及希望包含的注释类型。指令既可用于整个仓库，也可按任务上下文用于特定文件类型。

指令文件分为两类：

- `.github/copilot-instructions.md`：仓库级单个指令文件，会随每个仓库请求发送给 Copilot。它应包含适用于大多数 Copilot Chat 或 CLI 请求的项目信息，如技术栈、项目概述、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：可用于特定任务或文件类型。你可以使用它们为特定语言（如 TypeScript 或 Astro）或任务（如创建 UI 组件或新增单元测试）提供指导。

> [!NOTE]
> 在 IDE 中工作时，指令文件仅用于 Copilot Chat 的代码生成，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时都会使用仓库级指令文件和带 `applyTo` frontmatter 的 `*.instructions.md`文件。
>
> Copilot [支持使用其他标准的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

创建指令文件的完整讨论超出本研讨会范围。不过，示例项目中的示例体现了有代表性的做法。在较高层面：

- 在 `copilot-instructions.md`中聚焦项目级指导，例如项目构建内容、项目结构和全局编码标准。
- 使用 `*.instructions.md`为文件类型（单元测试、Astro组件、数据层）或特定任务提供具体指令。
- 使用自然语言，并保持指导清晰。提供代码应当和不应当呈现的示例。

创建指令文件的方法并非唯一，就像使用 AI 的方法也不唯一一样。通过实验，你会找到最适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应具备完善的指令文件集合。在探索本项目中的文件时，你会看到针对多种任务的文件，包括 [UI 更新][ui-instructions]和 [Astro][astro-instructions]。
>
> Copilot 也可帮助生成指令文件。每个界面呈现方式略有不同（例如，在 VS Code 中选择 **Configure Chat → Generate Agent Instructions**，或在 Copilot CLI 中运行 `/init`）；本课将在相关位置指出当前界面的操作。
>
> 需要模板或起点？可探索 [awesome-copilot][awesome-copilot]，其中包含指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 探索此项目中的自定义指令文件

花些时间阅读此仓库附带的指令文件：一个核心 `copilot-instructions.md`以及针对各种任务的 `*.instructions.md`集合。在编辑器或 GitHub 网页界面中打开它们。

1. 打开 `.github/copilot-instructions.md`。
2. 浏览该文件，注意项目简述以及 **Agent notes**、**Code standards**、**Scripts**和 **Repository Structure**等部分。在 **Code standards**中注意嵌套的 **GitHub Actions Workflows**指导。这些指令适用于你与 Copilot 的所有交互。
3. 打开 `.github/instructions`文件夹并浏览其中的文件。注意其中包含 Astro 文件、Drizzle 数据层、测试等方面的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。注意顶部的 `applyTo`字段；它设置一个相对于仓库根目录的 glob，用于决定指令适用于哪些文件。在此示例中，任何 TypeScript 测试文件（例如匹配 `**/*.test.ts`的文件）都会应用该指令。
5. 注意为当前项目创建单元测试而设置的指令。
6. 最后打开 `.github/instructions/drizzle.instructions.md`并滚动到底部。注意其他指令文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将大型指令集拆分为更小、可复用的文件，并在 Copilot 生成代码时指向可遵循的示例。（其中的路径相对于指令文件，而不是仓库根目录。）

> [!NOTE]
> `copilot-instructions.md`中的 **Code formatting requirements**部分记录了项目编码标准，但尚未要求提供代码内文档。下一步中，你将添加 TSDoc 文档注释和文件注释标题规则。

## 添加新的仓库标准

下一步是本处唯一需要编辑的部分：添加项目级规则，要求文档以 TSDoc 文档注释和文件级注释标题形式存在于代码中。云智能体以后处理分配给它的议题时会读取此规则。

编辑前，请先创建工作分支（云智能体会从议题目标分支读取指令，但仍应整洁地提交更改）：

1. 在 Codespace终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

如前所述，`.github/copilot-instructions.md`旨为 Copilot 提供项目级信息。现在确保仓库编码标准得到记录，以改进代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements**部分，它通常位于第 27 行附近。注意该部分记录了项目编码标准，但没有要求代码内文档，因此此前生成的辅助函数没有文档注释。
3. 在现有标准正下方添加以下 Markdown 行，要求 Copilot 添加文件注释标题和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 前一课已经说明，指令文件可在仓库级创建（`.github/copilot-instructions.md`）以提供全局指导，也可通过 `*.instructions.md`为特定语言、文件类型或任务提供指导。刚添加的文档注释规则属于项目级标准，应放在仓库级文件中。

## 提交、推送并合并指令更新

云智能体从议题目标分支读取指令文件。在下一练习中将议题分配给 Copilot 时，Copilot 会从 `main`创建分支，因此指令更改必须合并到 `main`才能生效。

1. 暂存并提交：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上从 `custom-instructions-cloud`向 `main`打开拉取请求并合并。之后，云智能体处理下一练习中分配的议题时会读取这些指令。

> [!TIP]
> 如果希望在本研讨会中直接使用 `main`，可跳过分支，直接提交到 `main`。分支步骤用于让研讨会贴近真实项目的处理方式。

## 总结与后续步骤

你已探索 Copilot 如何从当前项目的指令文件获取上下文，并向 `.github/copilot-instructions.md`添加了新的仓库级标准。在本流程剩余部分生成的拉取请求中，你将看到该标准的实际效果。

接下来，你将[将第一个议题分配给 Copilot 云智能体][next-lesson]。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更佳 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot——指令文件及其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
