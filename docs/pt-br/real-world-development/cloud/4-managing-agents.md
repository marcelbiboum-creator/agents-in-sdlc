---
title: "Exercício 4 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Nos exercícios anteriores, você pediu ao agente de nuvem do Copilot que assumisse três tarefas separadas voltadas à melhoria da experiência do usuário e à inclusão de funcionalidades. Embora o agente de nuvem tenha sido criado para operar de forma assíncrona e autônoma, a capacidade de monitorar essas tarefas continua sendo importante.

Há várias ferramentas disponíveis para gerenciar tarefas atribuídas ao agente de nuvem, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse Mission control, você pode visualizar todas as tarefas dos agentes com pull requests abertos, explorar as operações realizadas e até orientar uma sessão em andamento.

Neste exercício, você irá:

- explorar a página de agentes para acompanhar tarefas do agente de nuvem.
- orientar uma sessão em execução para solicitar uma funcionalidade adicional.

## Cenário

Depois de atribuir ao agente a criação de um modo de alto contraste, a equipe considerou que seria adequado adicionar também um modo claro. Como o trabalho já estava atualizando o estilo do site e adicionando controles de alternância, fazia sentido incluir essa funcionalidade. Você deseja orientar o trabalho do agente para que ele adicione tanto o modo claro quanto o alto contraste.

## Revise as tarefas do agente de nuvem do Copilot

Vamos ver o status atual de todas as tarefas atribuídas ao agente de nuvem do Copilot.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Observe a lista de tarefas no painel principal e no painel esquerdo. Você deverá ver as tarefas atribuídas ao Copilot, incluindo:
   - atualização da documentação da base de código;
   - geração de APIs para modificar jogos;
   - inclusão de um modo de alto contraste no site.
3. Selecione uma das tarefas em execução. Revise as operações realizadas pelo Copilot, que podem incluir:
   - obtenção do código do repositório;
   - criação do ambiente de trabalho;
   - configuração de servidores MCP;
   - execução de várias etapas para concluir a tarefa.

> [!NOTE]
> As etapas exatas variam conforme o estado do trabalho e a abordagem usada pelo Copilot.

4. Observe também o painel de pull request à direita. Ele permite acompanhar o PR e os arquivos alterados.

## Oriente o agente de nuvem

Agora que você viu as tarefas ativas, vamos pedir ao Copilot que inclua o modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão relacionada à inclusão do modo de alto contraste. O título exato pode variar conforme o nome usado pelo Copilot e o estado atual do trabalho.

   ![Sessão de acessibilidade no Mission control](../../../_images/ex6-accessibility-session.png)

2. Observe a sessão por alguns minutos, até ela indicar que concluiu a configuração e iniciou o trabalho.
3. Na caixa de diálogo **Steer active session while Copilot is working**, adicione o seguinte prompt:

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Captura de tela da tarefa do agente de nuvem com a caixa de diálogo de orientação destacada](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe como o Copilot reconhece o prompt e o incorpora ao fluxo de trabalho.

## Deixe o Copilot trabalhar

Como antes, o Copilot continuará trabalhando na tarefa atualizada. Ele incorporará o novo pedido ao fluxo depois de concluir a etapa específica em que estava quando você enviou a mensagem.

Como antes, isso levará alguns minutos, portanto é um bom momento para pausar e refletir sobre tudo que você aprendeu e explorou até agora.

## Resumo e próximos passos

Esta lição apresentou a página de agentes do Copilot, o central de monitoramento e orientação das tarefas do agente de nuvem do GitHub Copilot. Nesse Mission control, você pode acompanhar todas as tarefas ativas e concluídas, revisar o trabalho realizado e até redirecionar tarefas em andamento.

Você explorou estes conceitos:

- como usar o Mission control e a página de agentes para monitorar tarefas do agente de nuvem;
- como redirecionar uma sessão em execução para solicitar funcionalidades adicionais.

Com o Copilot concluindo o trabalho das funcionalidades de acessibilidade, agora podemos [iterar sobre os pull requests criados pelo Copilot][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
