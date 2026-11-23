---
title: "Exercício 5 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Agentes personalizados][previous-lesson] |
|:--|

Quando você coloca o GitHub Copilot no modo de agente, ele trabalha de forma autônoma: explora o código, sugere alterações, edita arquivos e executa comandos. Como esse trabalho ocorre em seu computador em tempo real, o Copilot Chat no VS Code mostra cada chamada de ferramenta e alteração de arquivo. Você pode revisar diffs, aceitar ou rejeitar alterações individuais e orientar a conversa com prompts de acompanhamento.

Neste exercício, você irá:

- monitorar o trabalho do agente de acessibilidade em tempo real;
- revisar e aceitar os arquivos propostos;
- orientar o agente durante a sessão para adicionar um modo claro junto ao modo de alto contraste.

## Cenário

O agente personalizado de acessibilidade usado no [Exercício 4][previous-lesson] está implementando o modo de alto contraste. Enquanto o trabalho está em andamento, a equipe de design solicita também um modo claro para pessoas que consideram o tema padrão muito escuro. Você orientará a sessão existente para ampliar o trabalho.

## Monitore o progresso do Copilot

O Copilot Chat mostra cada etapa: arquivos explorados, comandos executados e edições propostas.

1. Volte à visualização do Copilot Chat do Exercício 4.
2. Observe as chamadas de ferramentas e edições à medida que aparecem.
3. Para cada edição, use **Keep** para aceitar ou **Undo** para revertê-la e solicitar outra versão.
4. Use o indicador **Files changed** para ver o conjunto completo de arquivos modificado.

> [!NOTE]
> Se uma chamada de ferramenta pedir autorização, por exemplo para executar um comando no terminal, aprovar somente os comandos que você considerar adequados.

5. Aguarde o agente terminar o modo de alto contraste e mostrar um resumo das alterações.

## Oriente o agente para adicionar o modo claro

Agora que o modo de alto contraste está pronto, estenda a mesma conversa para adicionar o modo claro.

1. Envie o seguinte prompt no Copilot Chat:

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. O agente continuará a partir do trabalho já realizado e proporá adições para o modo claro.
3. Revise cada alteração usando **Keep** ou **Undo**.
4. Se o agente seguir uma direção indesejada, use o botão **Stop** e envie uma mensagem esclarecendo o ajuste.

> [!TIP]
> Orientar uma sessão em andamento é mais rápido do que recomeçar. Use prompts de acompanhamento para simplificar CSS, corrigir uma decisão ou ampliar o escopo.

## Revise o conjunto de alterações

Antes de confirmar o trabalho:

1. Abra a visualização **Source Control** no VS Code.
2. Revise todos os arquivos alterados.
3. Abra alguns diffs e confirme padrões de acessibilidade: atributos ARIA, navegação por teclado, HTML semântico e persistência via armazenamento local.
4. Quando estiver satisfeito, prepare e confirme as alterações no painel Source Control.

## Resumo e próximos passos

Você usou o modo de agente do Copilot Chat para monitorar e orientar uma sessão em andamento, aceitar ou rejeitar alterações e enviar prompts de acompanhamento.

Nesta lição, você explorou:

- monitorar o trabalho de um agente em tempo real;
- aceitar e rejeitar edições individuais;
- orientar uma sessão em andamento.

Na [próxima lição][next-lesson], você publicará o trabalho de acessibilidade em um pull request e revisará as alterações produzidas pelo agente personalizado.

## Recursos

- [Copilot Chat no VS Code][copilot-chat-vscode]
- [Usar o modo de agente][agent-mode]

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
