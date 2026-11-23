---
title: "Exercício 4 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## O que são agentes personalizados?

Os [agentes personalizados][custom-agents-concept] no GitHub Copilot permitem criar assistentes de IA especializados para tarefas ou áreas específicas do fluxo de desenvolvimento. Ao definir agentes por meio de arquivos Markdown na pasta `.github/agents` do repositório, você pode fornecer ao Copilot instruções, boas práticas, padrões de código e conhecimento específico do domínio.

Os agentes personalizados são definidos por arquivos Markdown na pasta `.github/agents` do projeto ou globalmente em `~/.copilot/agents`. Cada arquivo tem frontmatter YAML com `name` e `description`, seguido de um prompt Markdown.

> [!NOTE]
> Não existe uma única forma correta de criar um agente personalizado. Teste e itere para descobrir o que funciona melhor.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents

## Cenário

A Tailspin Toys quer garantir que sua plataforma de financiamento coletivo seja acessível a todas as pessoas. Comentários recentes indicaram que algumas pessoas consideram o tema escuro difícil de ler devido ao contraste insuficiente. A equipe solicitou a implementação de um modo de alto contraste que possa ser ativado e desativado.

Neste exercício, você irá:

- revisar um agente personalizado de acessibilidade existente;
- usar o agente no Copilot Chat para implementar o modo de alto contraste.

## Revise o agente personalizado de acessibilidade

Um agente personalizado já foi criado para acessibilidade.

1. Volte ao codespace e abra um terminal.
2. Crie uma branch fresca a partir de `main`:

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

3. Abra `.github/agents/accessibility.md`.
4. Observe o frontmatter YAML com `name` e `description`.

> [!CAUTION]
> O frontmatter com `name` e `description` é obrigatório.

5. Revise as seções sobre responsabilidades principais, boas práticas, exemplos de HTML/CSS/JavaScript e armadilhas comuns.

## Use o agente personalizado no Copilot Chat

O VS Code mostra os agentes personalizados definidos em `.github/agents` no seletor de agentes do Copilot Chat.

1. Selecione **Agent** no seletor se ele ainda não estiver ativo.
2. Selecione **Accessibility agent**.
3. Envie o seguinte prompt:

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

4. O Copilot explorará o código, proporá alterações e editará os arquivos do projeto.

> [!NOTE]
> O processo pode levar alguns minutos. O Copilot editará componentes Astro, CSS e testes relacionados.

Você revisará e orientará esse trabalho no próximo exercício.

## Resumo e próximos passos

Você revisou um agente personalizado especializado em acessibilidade e preparou seu uso no Copilot Chat.

Em seguida, [monitore e oriente o trabalho do agente][next-lesson], revise as alterações à medida que elas acontecem e adicione um modo claro à mesma sessão.

## Recursos

- [Sobre agentes personalizados][custom-agents]
- [Criar agentes personalizados no seu IDE][creating-custom-agents-ide]
- [Agentes personalizados no VS Code][custom-agents-vscode]

| [← Lição anterior: Testar com o Playwright MCP][previous-lesson] | [Próxima lição: Monitorar e gerenciar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
