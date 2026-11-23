---
title: "练习 0：先决条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 Visual Studio Code 和 GitHub Copilot 练习之前，需要准备好环境。你将创建 Tailspin Toys 仓库的副本，并启动一个用于编辑指令文件和审查 Copilot 工作成果的 [Codespace][codespaces]。

## 设置实验室仓库

要为即将编写的代码创建仓库副本，请根据 [模板][template-repository]创建实例。新实例将包含实验所需的全部文件，后续练习会始终使用它。

1. 在新的浏览器窗口中，导航到 [Tailspin Toys 模板][tailspin-template]。
2. 在实验室仓库页面选择 **Use this template** 按钮，从而创建仓库副本，然后选择 **Create new repository**。

    ![Use this template 按钮](../../../_images/ex0-use-template.png)

3. 如果你正在参加由 GitHub 或 Microsoft组织的研讨会，请按照导师的说明操作。否则，请在自己能够使用 GitHub Copilot 的组织中创建仓库。

    ![输入仓库模板设置](../../../_images/ex0-repository-settings.png)

4. 记下你创建的仓库路径（**organization-or-user-name/repository-name**），后续实验中会用到。

## 创建 Codespace

接下来，使用 Codespace完成实验练习。

[GitHub Codespaces][codespaces]是一种云端开发环境，你可以直接在浏览器中编写、运行和调试代码。它提供完整的 IDE，并支持多种编程语言、扩展和工具。

1. 导航到新建的仓库。
2. 选择绿色的 **Code**按钮。

    ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces**选项卡，然后选择 **+**按钮创建新的 Codespace。

    ![创建新的 Codespace](../../../_images/ex0-create-codespace.png)

Codespace的创建需要几分钟，但仍比手动安装全部服务快得多！在等待期间，可以探索 GitHub Copilot的其他功能，我们将在下一步介绍。

> [!CAUTION]
> 后续练习中会再次使用该 Codespace。暂时请将其留在浏览器标签页中，不要删除。

> [!NOTE]
> 本研讨会可在 Codespace或本地[开发容器][dev-containers]中运行。两者都会确保环境中预装必要的先决条件，提供流畅的体验。如果希望在本地运行，请打开克隆后的仓库，在出现提示时选择 **Reopen in Container**；VS Code将构建与 Codespace相同的开发容器。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## 总结

恭喜，你已创建实验室仓库的副本！你也已开始创建 Codespace，后续将用于完成练习并审查 Copilot的工作。

## 下一步

接下来，添加 GitHub Copilot遵循的自定义指令。继续学习[练习 1：自定义指令][next-lesson]。

## 资源

- [GitHub Codespaces概述][codespaces]
- [从模板创建仓库][template-repository]
- [开始使用 Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
