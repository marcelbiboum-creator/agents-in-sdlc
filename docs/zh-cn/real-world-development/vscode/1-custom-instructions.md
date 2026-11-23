---
title: "练习 1——自定义指令（VS Code）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：智能体模式 →][next-lesson]

与生成式 AI协作时，上下文至关重要。如果任务需要特定方式完成，或 Copilot 应了解某些背景信息，就应确保这些上下文可被获取。[指令文件][instruction-files]是向 Copilot 提供代码生成指导的主要方式。

在本练习中，你将：

- 探索项目上下文、编码规范和文档标准如何通过仓库自定义指令及按路径限定的指令文件传递给 Copilot。
- 在现有指令下生成筛选所需的第一片数据（发布商辅助函数）。
- 在 `.github/copilot-instructions.md`中添加新的仓库级标准。
- 重新运行相同提示，观察生成代码采用新标准。
- 将指令更新和筛选片段提交到 `main`，让 Copilot 在下一练习中使用更新后的指导。

> [!CAUTION]
> 生成代码可能偏离你设定的某些标准；Copilot具有非确定性。本练习的重点是观察更新指令后行为变化的趋势，而不是逐字符匹配输出。

## 指令文件

### 场景

作为优秀的开发团队，Tailspin Toys 为开发实践制定了一套规范，其中包括：

- 数据层始终需要单元测试。
- 界面应采用深色模式并呈现现代感。
- 应以 TSDoc文档注释形式为代码添加文档。
- 应在每个文件顶部添加注释块，说明文件用途。

通过指令文件，你可以确保 Copilot 获得符合上述实践所需的信息。

### 自定义指令

自定义指令允许你向 Copilot 提供上下文和偏好，使它更好地理解编码风格和需求。这项强大功能可帮助你引导 Copilot 提供更相关的建议和代码片段。你可以指定首选编码约定、库，以及希望包含的注释类型。指令既可用于整个仓库，也可按任务上下文用于特定文件类型。

指令文件分为两类：

- `.github/copilot-instructions.md`：仓库级单个指令文件，会随仓库中的每次请求发送给 Copilot。它应包含适用于大多数聊天或 CLI请求的项目信息，如技术栈、项目概述、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：可用于特定任务或文件类型。你可以为特定语言（如 TypeScript 或 Astro）或任务（如创建 UI组件或一组单元测试）提供指导。

> [!NOTE]
> 在 IDE 中工作时，指令文件仅用于 Copilot Chat的代码生成，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时都会使用仓库级指令文件和带 `applyTo`frontmatter 的 `*.instructions.md`文件。
>
> Copilot [支持使用其他标准的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

创建指令文件的完整讨论超出本研讨会范围。示例项目中的示例展示了一种代表性方法：

- 在 `copilot-instructions.md`中聚焦项目级指导，例如项目构建内容、项目结构和全局编码标准。
- 使用 `*.instructions.md`为文件类型（单元测试、Astro组件、数据层）或特定任务提供具体指令。
- 使用自然语言，保持指导清晰，并提供代码应当和不应当呈现的示例。

没有唯一的指令文件创建方式，也没有唯一的 AI使用方式。通过实验，你会找到最适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应具备完善的指令文件集合。在探索本项目中的文件时，你会看到针对多种任务的文件，包括 [UI 更新][ui-instructions]和 [Astro][astro-instructions]。
>
> Copilot 也可帮助生成指令文件。每个界面的呈现方式略有不同（例如，在 VS Code中选择 **Configure Chat → Generate Agent Instructions**，或在 Copilot CLI中运行 `/init`）。
>
> 需要模板或起点？可探索 [awesome-copilot][awesome-copilot]，其中包含指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 探索此项目中的自定义指令文件

花些时间阅读此仓库附带的指令文件：一个核心 `copilot-instructions.md`以及针对各种任务的 `*.instructions.md`集合。在编辑器或 GitHub 网页界面中打开它们。

1. 打开 `.github/copilot-instructions.md`。
2. 浏览该文件，注意项目简述以及 **Agent notes**、**Code standards**、**Scripts**和 **Repository Structure**等部分。在 **Code standards**中注意嵌套的 **GitHub Actions Workflows**指导。这些适用于你与 Copilot 的所有交互。
3. 打开 `.github/instructions`文件夹并浏览。注意其中包含 Astro 文件、Drizzle 数据层、测试等方面的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。注意顶部的 `applyTo`字段；它设置相对于仓库根目录的 glob，用于决定指令适用于哪些文件。此处任何 TypeScript 测试文件（例如匹配 `**/*.test.ts`的文件）都会应用该指令。
5. 注意为此项目创建单元测试而设置的指令。
6. 最后打开 `.github/instructions/drizzle.instructions.md`并滚动到底部。注意其他指令文件（如 `unit-tests.instructions.md`）和现有项目文件的链接。这样可以拆分大型指令集，并指向生成代码时可遵循的示例。（其中的路径相对于指令文件，而不是仓库根目录。）

> [!NOTE]
> `copilot-instructions.md`中的 **Code formatting requirements**部分记录了项目编码标准，但尚未要求代码内文档。下一步中，你将添加 TSDoc文档注释和文件注释标题规则。

## 为更改创建分支

现在使用分支遵循一些最佳实践。

1. 返回前一练习中的 Codespace。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端。
3. 创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions
   ```

## 在更新指令前使用 Copilot Chat

> [!TIP]
> **打开 Copilot Chat**
>
> 开始下面的练习前，返回 Codespace，打开 Copilot Chat面板，并选择 **New Chat**开始全新对话。

为观察自定义指令的影响，先在现有指令文件中发送提示。稍后更新指令并重新发送相同提示，以查看差异。

1. 关闭前面练习的编辑器标签页，让 Copilot仅获取所需上下文。
2. 打开 `src/lib/publishers.ts`，让 Copilot知道辅助函数应放在哪里。
3. 在 Chat视图的智能体下拉列表中选择 **Agent**，让 Copilot应用文件更改。

   ![Chat视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

4. 发送以下提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot探索项目并应用代码更新，通常会涉及辅助函数文件及其测试。
6. 注意生成的辅助函数是类型化函数，首个参数是 `db`客户端，并返回类型化的发行商数组；这是 `.github/instructions/drizzle.instructions.md`（适用于 `src/lib/*.ts`）中的数据层约定。
7. 注意生成代码缺少 TSDoc文档注释和文件级注释标题。

> [!CAUTION]
> 由于 Copilot具有概率性，即使未要求，它也可能添加文档注释。如果发生这种情况，仍可继续；更新指令后的一致性改进才是本练习重点。

## 添加新的仓库标准

如前所述，`.github/copilot-instructions.md`旨在为 Copilot 提供项目级信息。现在记录仓库编码标准，以改进代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到约位于第 27 行附近的 **Code formatting requirements**部分。注意该部分记录了项目编码标准，但没有要求代码内文档，这也是生成的辅助函数缺少注释的原因。
3. 在现有标准正下方添加以下 Markdown 行，要求 Copilot 添加文件注释标题和 TSDoc文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 与前面课程一样，仓库级指令应放在 `.github/copilot-instructions.md`中，特定语言、文件类型或任务可使用 `*.instructions.md`。刚添加的文档注释规则属于项目级标准，因此应放在仓库级文件中。

## 重新运行提示并观察变化

1. 返回 Copilot Chat并选择 **New Chat**清除缓冲区。
2. 返回 `src/lib/publishers.ts`，让 Copilot聚焦正确文件。
3. 发送与前面相同的提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 注意生成文件现在以类似以下注释块开头：

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 注意生成函数现在包含类似以下的 TSDoc注释：

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

你刚引导 Copilot 遵循新的项目标准，并将它应用于后续练习将继续使用的真实代码。

## 提交指令并推送分支

指令文件与仓库中的其他资产一样，应使用相同的源代码管理方式管理。现在提交并推送分支。

1. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端窗口。
2. 在终端中运行以下命令，确认指令更新和辅助函数更改已存在：

   ```bash
   git status
   ```

3. 暂存并提交指令更新及 Copilot 为辅助函数基础更改的所有文件：

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # 如果 git status 显示其他支持性更新（例如测试），也请添加这些文件。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. 推送分支：

   ```bash
   git push -u origin custom-instructions
   ```

## 创建并合并拉取请求

分支推送后，应创建拉取请求，并将它关联到待办事项中的文档标准议题。可以手动操作，也可以使用项目中已连接的 GitHub工具让 Copilot代办。

> [!NOTE]
> 这是 Copilot首次代表你在 GitHub 上执行操作。项目模板已将 GitHub工具连接到工作区，无需额外设置；Copilot首次使用工具时，VS Code可能提示登录 GitHub。请按照提示授权。

1. 在 Codespace中打开 Copilot Chat。
2. 按 <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd>（Windows/Linux）打开 Copilot Chat，并确保智能体选择器中已选择 **Agent**。
3. 请 Copilot 找到更新指令文件相关的议题，并从当前分支创建 PR，以说明指令更新和新的发布商辅助函数基础：

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot开始查找议题并创建 PR。
5. 当系统提示 **Allow**Copilot代表你执行 GitHub操作时，请审查命令并酌情选择 **Allow**。
6. PR创建后，请 Copilot合并 PR，并使用以下提示将分支返回到 main：

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. 当系统提示 **Allow**Copilot代表你执行 GitHub操作和运行 shell命令时，请审查命令并酌情选择 **Allow**。

现在，你已借助 GitHub Copilot创建并合并了拉取请求！

## 总结与后续步骤

你已探索 Copilot 如何从此项目的指令文件获取上下文，并使用 VS Code中的 Copilot Chat：

- 发送代码生成提示并观察现有指令下的 Copilot输出。
- 在 `.github/copilot-instructions.md`中添加新的仓库级标准。
- 重新运行相同提示并观察建议代码采用新标准。
- 将指令更新和辅助函数基础提交到 `main`，供下一练习构建。

接下来，你将在[智能体模式][next-lesson]中应用这些指令，让 Copilot跨代码库添加新功能。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更佳 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [GitHub Copilot 的个人自定义指令][personal-instructions]
- [Awesome Copilot——指令文件及其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
