---
title: "Exercício 0: Pré-requisitos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de começar os exercícios do agente de nuvem do Copilot, você precisa preparar tudo. Criará sua própria cópia do repositório Tailspin Toys e iniciará um [codespace][codespaces] que poderá usar para editar arquivos de instruções e revisar o trabalho produzido pelo agente de nuvem.

## Prepare o repositório do laboratório

Para criar uma cópia do repositório em que fará o código, você criará uma instância a partir do [template][template-repository]. A nova instância conterá todos os arquivos necessários para o laboratório e será usada ao longo dos exercícios.

1. Em uma nova janela do navegador, acesse o [template da Tailspin Toys][tailspin-template].
2. Crie sua própria cópia do repositório selecionando o botão **Use this template** na página do repositório de laboratório. Depois, selecione **Create a new repository**.

   ![Botão Use this template](../../../_images/ex0-use-template.png)

3. Se estiver participando de um workshop conduzido pelo GitHub ou pela Microsoft, siga as instruções fornecidas pelas pessoas responsáveis. Caso contrário, crie o novo repositório em uma organização na qual tenha acesso ao GitHub Copilot.

   ![Configurações do repositório criado a partir do template](../../../_images/ex0-repository-settings.png)

4. Anote o caminho do repositório que criou (**organization-or-user-name/repository-name**), pois você precisará dele mais tarde no laboratório.

## Crie um codespace

Em seguida, você usará um codespace para concluir os exercícios do laboratório.

O [GitHub Codespaces][codespaces] é um ambiente de desenvolvimento baseado em nuvem que permite escrever, executar e depurar código diretamente no navegador. Ele fornece um IDE completo com suporte a várias linguagens de programação, extensões e ferramentas.

1. Acesse o repositório recém-criado.
2. Selecione o botão verde **Code**.

   ![Selecione o botão Code](../../../_images/ex0-code-button.png)

3. Selecione a aba **Codespaces** e o botão **+** para criar um novo Codespace.

   ![Crie um novo codespace](../../../_images/ex0-create-codespace.png)

A criação do codespace pode levar alguns minutos, embora ainda seja muito mais rápido do que instalar manualmente todos os serviços. Você pode usar esse tempo para explorar outros recursos do GitHub Copilot, tema para o qual direcionaremos sua atenção a seguir.

> [!CAUTION]
> Você retornará ao codespace em um exercício futuro. Por enquanto, deixe-o aberto em uma aba do navegador.

> [!NOTE]
> Este workshop foi desenvolvido para ser executado dentro de um codespace ou de um [dev container][dev-containers] local. Ambos garantem que o ambiente tenha todos os pré-requisitos necessários para uma experiência tranquila. Se preferir executar localmente, abra o repositório clonado no VS Code e selecione **Reopen in Container** quando solicitado; o VS Code criará o mesmo dev container usado pelo codespace.

## Resumo

Parabéns! Você criou uma cópia do repositório do laboratório e iniciou o processo de criação do codespace que usará ao trabalhar com o agente de nuvem do Copilot.

## Próximo passo

Vamos adicionar instruções personalizadas que o agente de nuvem seguirá. Continue para o [Exercício 1 - Instruções personalizadas][next-lesson].

## Recursos

- [Visão geral do GitHub Codespaces][codespaces]
- [Criar um repositório a partir de um template][template-repository]
- [Introdução ao Codespaces][codespaces-quickstart]

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
