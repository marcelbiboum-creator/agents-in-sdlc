---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Use o Plan para concordar com uma abordagem, o Autopilot para criar a filtragem a partir de uma issue e o modo Interactive para revisar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Começamos adicionando uma funcionalidade pequena ao projeto. Alterações maiores exigem um processo mais robusto. Felizmente, o GitHub Copilot CLI foi criado para trabalhar com o fluxo existente de uma organização, garantindo que construamos as coisas certas da maneira certa. Esta é a primeira de várias lições em que você seguirá um processo típico de desenvolvimento orientado por agentes, começando pelo uso de uma issue para gerar uma nova funcionalidade, garantindo que o código seja válido, que a funcionalidade se comporte como esperado e que ela seja mesclada com sucesso ao projeto.

> [!NOTE]
> Você usará a mesma conversa e a mesma branch enquanto continua pelo fluxo da funcionalidade. Normalmente, você teria branches ou PRs diferentes para os diferentes tipos de arquivo em que trabalha, mas usaremos um atalho para nos concentrarmos nos conceitos principais.

Para começar, nesta lição, você irá:

- iniciar uma nova conversa do Copilot a partir de uma issue do GitHub.
- definir os requisitos no modo Plan.
- implementar a nova funcionalidade no modo Autopilot.
- revisar o código.
- validar a funcionalidade manualmente em um navegador encaminhado.

À medida que continuar esta funcionalidade, você atualizará as instruções do repositório, personalizará a skill existente `quality-checks`, adicionará a validação MCP, criará um agente de QA e abrirá o PR da funcionalidade.

## Cenário

O catálogo da Tailspin Toys está crescendo, e os visitantes precisam restringir os jogos por categoria e editora. A issue do backlog descreve a funcionalidade, mas detalhes como a combinação de categorias exigem alinhamento antes da implementação. Você usará o modo Plan para resolver essas decisões e depois autorizará uma implementação limitada com o Autopilot.

## Contexto

Introduzir agentes de codificação de IA no fluxo de desenvolvimento não altera os fundamentos. Na verdade, eles se tornam ainda mais importantes. A maioria das pessoas desenvolvedoras segue um fluxo semelhante a:

1. Começar por uma issue registrada que descreve o que precisa ser feito.
2. Criar um plano do que deve ser desenvolvido.
3. Criar e revisar o código.
4. Executar os testes para validar o código.
5. Validar manualmente a nova funcionalidade.
6. Criar um pull request (PR).
7. Depois que o código for revisado e o processo de integração contínua terminar, mesclar o código.

> [!NOTE]
> Dependendo da sua equipe e organização, os detalhes exatos podem variar, mas a maioria seguirá uma versão do fluxo descrito acima.

Ao seguir essa abordagem padrão, você garante que o código gerado por IA atende aos requisitos estabelecidos e passa pelo mesmo processo de verificação de código escrito manualmente.

## Modos de conversa

O **modo de conversa** controla o nível de autonomia do agente. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar entre os modos:

- **Interactive**: você e o agente trabalham juntos. O agente sugere alterações e aguarda sua entrada antes de prosseguir.
- **Plan**: o agente cria um plano primeiro e não pode editar arquivos do projeto.
- **Autopilot**: o agente trabalha de forma autônoma — escreve código, executa testes e itera até concluir a tarefa.

Comece no modo Plan, revise o plano e use o Autopilot para implementá-lo.

## Comece pela issue

Antes de iniciar o trabalho de filtragem, retorne ao Codespace e confirme que o repositório e o terminal estão prontos.

1. Volte ao seu Codespace. Se ele estiver parado, reinicie-o antes de continuar.
2. Confirme que o PR das avaliações por estrelas foi mesclado.
3. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Atualize `main` e crie uma branch para o trabalho de filtragem:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicie o Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pressione <kbd>Tab</kbd> duas vezes para abrir a aba **Issues**.
7. Pressione <kbd>A</kbd> para mostrar todas as issues.
8. Use as teclas de direção para destacar a issue intitulada **Allow users to filter games by category and publisher**.
9. Pressione <kbd>C</kbd> para adicionar a issue ao prompt e retornar à aba **Session**.

Observe que o prompt começa com `#7` ou um número semelhante. O `#` permite incorporar uma issue ou um pull request (PR) do GitHub ao contexto.

## Planeje a funcionalidade de filtragem

O planejamento permite definir a abordagem para implementar uma funcionalidade ou executar tarefas antes de entregá-las ao Copilot. É sempre uma boa ideia reservar um tempo para planejar qualquer trabalho complexo. Vamos alternar para o modo Plan e pedir ao Copilot que crie o plano.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar para o modo Plan. Confirme que o indicador de modo abaixo do prompt mostra **Plan**.
2. Depois da referência à issue adicionada na etapa anterior, digite o seguinte prompt:

   ```plaintext
   Create a plan for implementing this feature.
   ```

O Copilot começará a montar o plano. Primeiro, explorará o projeto e, depois, determinará a melhor abordagem.

3. Durante o processo, o Copilot pode fazer perguntas sobre como as capacidades de filtragem devem funcionar. Responda com base nas suas preferências. Não há respostas erradas aqui.
4. Quando o plano estiver concluído, pressione <kbd>Control</kbd>+<kbd>E</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandi-lo.
5. Role para cima e para baixo para revisar o plano.
6. Peça ao Copilot que revise qualquer parte do plano que não corresponda às suas decisões.

## Aprove o Autopilot

Com o plano escrito e revisado, é hora de implementá-lo. Vamos deixar o Copilot agir usando o Autopilot.

O Autopilot permite que o Copilot itere sobre o problema até considerar que a tarefa está concluída.

1. Selecione **Accept plan and build on autopilot (recommended)** ou a opção com rótulo semelhante na sua versão instalada.
2. Confirme que o indicador de modo abaixo do prompt mostra **Autopilot**.
3. Observe enquanto o Copilot itera pelo plano estabelecido, gera código e executa testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente, então revise o plano primeiro. Se o Copilot informar dependências ausentes ou conflito de porta, resolva o problema de configuração antes de considerar as verificações concluídas.

## Revise e verifique a implementação

Depois que o código é gerado, ele precisa ser revisado antes do merge, como qualquer outro código. Vamos revisar o código e executar o site para garantir que tudo esteja correto.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar no modo Interactive. Confirme que o indicador de modo não mostra mais **Plan** nem **Autopilot**.
2. Digite `/diff` e inspecione a implementação da filtragem e os testes.
3. Compare o resultado com a issue e as decisões tomadas durante o planejamento.
4. Depois de revisar o código, pressione <kbd>Esc</kbd> para sair da visualização de diff.
5. Revise a saída das verificações do projeto e peça ao Copilot que resolva qualquer falha.

## Explore a nova funcionalidade

O código parece bom — mas será que ele funciona? Vamos iniciar o aplicativo como antes e abrir o site pela porta encaminhada do Codespaces.

1. Peça ao Copilot que inicie o aplicativo:

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Experimente a filtragem por categoria, a filtragem por editora e as combinações acordadas no plano.
4. Confirme que o comportamento de redefinição e de resultados vazios corresponde à issue e às suas decisões.
5. Volte ao Codespace e peça ao Copilot que pare o servidor de desenvolvimento iniciado.

## Resumo e próximos passos

Você usou diferentes modos de conversa para criar e revisar uma funcionalidade. Nesta lição, você:

- iniciou uma nova conversa do Copilot a partir de uma issue do GitHub.
- definiu requisitos no modo Plan.
- implementou a nova funcionalidade no modo Autopilot.
- revisou o código.
- validou a funcionalidade manualmente em um navegador encaminhado.

Em seguida, vamos aprofundar a geração de código e garantir que ela siga as práticas documentadas, [usando instruções personalizadas][next-lesson].

## Recursos

- [Autopilot no GitHub Copilot CLI][autopilot]
- [Referência de comandos do Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
