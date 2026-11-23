---
title: "Exercício 0: Pré-requisitos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de começar os exercícios do VS Code, prepare tudo. Você criará sua própria cópia do repositório Tailspin Toys, iniciará um [codespace][codespaces] e confirmará que o GitHub Copilot Chat está funcionando no editor.

## Prepare o repositório do laboratório

Para criar uma cópia do repositório em que fará o código, crie uma instância a partir do [template][template-repository]. A nova instância conterá todos os arquivos necessários para o laboratório.

1. Em uma nova janela do navegador, acesse o [template da Tailspin Toys][tailspin-template].
2. Crie sua própria cópia selecionando **Use this template** e depois **Create a new repository**.

   ![Botão Use this template](../../../_images/ex0-use-template.png)

3. Se estiver participando de um workshop conduzido pelo GitHub ou pela Microsoft, siga as instruções fornecidas pelas pessoas responsáveis. Caso contrário, crie o repositório em uma organização na qual tenha acesso ao GitHub Copilot.

   ![Configurações do repositório criado a partir do template](../../../_images/ex0-repository-settings.png)

4. Anote o caminho do repositório criado (**organization-or-user-name/repository-name**).

> [!NOTE]
> **Seu backlog está pronto**
>
> Ao criar o repositório a partir do template, um backlog de issues do GitHub será criado automaticamente.

## Crie um codespace

O [GitHub Codespaces][codespaces] é um ambiente de desenvolvimento baseado em nuvem que permite escrever, executar e depurar código diretamente no navegador.

1. Acesse o repositório recém-criado.
2. Selecione o botão verde **Code**.

   ![Selecione o botão Code](../../../_images/ex0-code-button.png)

3. Selecione a aba **Codespaces** e o botão **+** para criar um novo Codespace.

   ![Crie um novo codespace](../../../_images/ex0-create-codespace.png)

> [!CAUTION]
> Você retornará ao codespace em um exercício futuro. Por enquanto, deixe-o aberto em uma aba do navegador.

> [!NOTE]
> Este workshop foi desenvolvido para executar dentro de um codespace ou de um [dev container][dev-containers] local. Ambos garantem que o ambiente tenha todos os pré-requisitos necessários.

## Use o GitHub Copilot Chat e o modo de agente

Para acessar o modo de agente do GitHub Copilot Chat, você precisa ter a extensão GitHub Copilot Chat instalada no IDE.

> [!TIP]
> Se a extensão não estiver instalada, você pode [instalá-la pela Visual Studio Code Marketplace][copilot-chat-extension]. Ou abra a visualização de Extensões no VS Code, procure **GitHub Copilot Chat** e selecione **Install**.

1. Volte ao codespace.
2. Se não estiver vendo o Copilot Chat à direita do editor, selecione o ícone **Copilot Chat** no topo do codespace.
3. Digite uma mensagem como "Hello world" na janela do Copilot Chat e pressione Enter.
4. Se não estiver autenticado, siga as instruções para entrar no GitHub.

   ![Exemplo de prompt de autenticação do Copilot Chat](../../../_images/ex1-copilot-authentication.png)

5. Depois da autenticação, a janela do Copilot Chat será exibida.

## Resumo

Parabéns! Você criou uma cópia do repositório do laboratório e iniciou o codespace que usará ao começar a escrever código.

## Próximo passo

Continue para o [Exercício 1 - Instruções personalizadas][next-lesson], onde você ensinará ao Copilot as convenções do projeto.

## Recursos

- [Visão geral do GitHub Codespaces][codespaces]
- [Criar um repositório a partir de um template][template-repository]
- [Introdução ao Codespaces][codespaces-quickstart]

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
