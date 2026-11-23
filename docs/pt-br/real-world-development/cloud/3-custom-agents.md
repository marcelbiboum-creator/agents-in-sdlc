---
title: "Exercício 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## O que são agentes personalizados?

Os [agentes personalizados][custom-agents-concept] no GitHub Copilot permitem criar assistentes de IA especializados para tarefas ou áreas específicas do fluxo de desenvolvimento. Ao definir agentes por meio de arquivos Markdown na pasta `.github/agents` do repositório, você pode fornecer ao Copilot instruções, boas práticas, padrões de código e conhecimento específico do domínio para executar determinados tipos de trabalho com mais eficiência. As equipes podem incorporar sua experiência em agentes reutilizáveis — por exemplo, um agente de acessibilidade que aplica as diretrizes [WCAG][wcag], um agente de segurança que segue práticas de programação segura ou um agente de testes que mantém padrões de teste consistentes.

Os agentes personalizados são definidos por arquivos Markdown na pasta `.github/agents` do projeto ou globalmente em `~/.copilot/agents`. Cada arquivo tem frontmatter YAML com pelo menos `name` e `description`, seguido de um prompt Markdown que define o comportamento, a área de especialização e as instruções do agente.

### Agentes personalizados comparados com skills de agente

Há alguma sobreposição lógica entre agentes personalizados e [skills de agente][agent-skills-concept]. Ambos são definidos principalmente por arquivos Markdown e indicam à IA como realizar operações. A forma mais clara de separá-los é: um **agente personalizado** é o trabalhador e as **skills** são ferramentas.

Os agentes personalizados têm sua própria janela de contexto e foram criados para orquestrar skills — e até outros agentes — ao executar o trabalho. Neste laboratório, o agente personalizado de acessibilidade revisa e atualiza o site conforme as diretrizes de acessibilidade. Nesse trabalho, ele pode usar skills como uma skill de fluxo de pull request ou outra que execute e gerencie testes.

> [!NOTE]
> Não existe uma única forma “correta” de criar um agente personalizado. Como em tudo relacionado a IA, teste e itere para descobrir o que funciona melhor em seus ambientes e cenários.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

Você explorará o seguinte com agentes personalizados:

- como os agentes personalizados são definidos;
- como atribuir uma tarefa a um agente personalizado.

## Cenário

A Tailspin Toys tem o compromisso de garantir que sua plataforma de financiamento coletivo seja acessível a todas as pessoas, independentemente de capacidades ou preferências visuais. Comentários recentes de usuários indicaram que algumas pessoas consideram o tema escuro atual difícil de ler devido ao contraste insuficiente entre texto e fundo. Para resolver essa questão de acessibilidade, a equipe de design solicitou a implementação de um modo de alto contraste que possa ser ativado e desativado.

Como a acessibilidade é fundamental, você quer garantir que ela seja implementada o mais rápido possível. Utilizará um agente personalizado para gerar a funcionalidade.

## Revise o agente personalizado de acessibilidade

Um agente personalizado já foi criado para acessibilidade. Vamos revisar seu conteúdo para entender como ele orientará o Copilot.

Volte ao codespace e revise o arquivo do agente personalizado de acessibilidade:

1. Abra `.github/agents/accessibility.md`.
2. Observe o frontmatter YAML com os campos `name` e `description`.

> [!CAUTION]
> O frontmatter com `name` e `description` é obrigatório para agentes personalizados.

3. Em seguida, revise as seções que destacam:
   - responsabilidades principais ao gerar código para um site acessível;
   - boas práticas de acessibilidade;
   - exemplos de código em HTML, CSS e JavaScript;
   - uma lista de armadilhas e erros comuns.

## Crie e atribua uma issue

O Mission control é o local central para trabalhar com todos os agentes do seu ambiente. Você pode atribuir tarefas ao Copilot, acompanhar tarefas e até redirecioná-las ou fornecer orientações adicionais. Vamos começar atribuindo uma tarefa para criar o modo de alto contraste ao Copilot.

1. Acesse seu repositório.
2. Selecione a aba **Issues**.
3. Selecione **New issue**.
4. Selecione **Blank issue**.
5. Defina o **Title** como `Add high contrast mode to website`.
6. Defina a **Description** como:

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

7. Selecione **Create**.
8. À direita, selecione **Assign to Copilot**.
9. Selecione **Accessibility agent** na lista de agentes personalizados.

   ![Captura de tela da atribuição ao agente de nuvem, com agente personalizado e Accessibility destacados](../../../_images/ex5-select-custom-agent.png)

10. Selecione **Assign**.
11. O Copilot começará a trabalhar na tarefa em segundo plano.

## Resumo e próximos passos

Esta lição explorou [agentes personalizados][custom-agents] no GitHub Copilot — assistentes de IA especializados adaptados a tarefas e áreas específicas. Com agentes personalizados, você pode incorporar a experiência e os padrões da equipe em agentes reutilizáveis que orientam o Copilot a executar determinados tipos de trabalho com mais eficiência.

Você explorou estes conceitos:

- como agentes personalizados são definidos;
- como atribuir uma tarefa a um agente personalizado.

Com o Copilot implementando o modo de alto contraste, podemos agora [monitorar e orientar a sessão do agente][next-lesson] a partir do Mission control.

## Recursos

- [Sobre agentes personalizados][custom-agents]
- [Preparar o uso de agentes personalizados em sua organização][org-custom-agents]
- [Preparar o uso de agentes personalizados em sua empresa][enterprise-custom-agents]

| [← Lição anterior: Agente de nuvem do GitHub Copilot][previous-lesson] | [Próxima lição: Monitorar e gerenciar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
