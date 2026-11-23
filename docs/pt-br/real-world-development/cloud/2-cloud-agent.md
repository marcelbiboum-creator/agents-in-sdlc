---
title: "Exercício 2 - Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Instruções personalizadas][previous-lesson] |
|:--|

Poucas organizações, talvez nenhuma, não enfrentem dificuldades com dívida técnica. Isso pode incluir problemas de segurança não resolvidos, código legado que precisa ser atualizado ou solicitações de funcionalidades que ficaram no backlog por falta de tempo para implementá-las. O agente de nuvem do GitHub Copilot foi criado para executar tarefas como atualizar código e adicionar funcionalidades de forma autônoma. Quando o agente conclui o trabalho, gera um PR em rascunho pronto para revisão por uma pessoa desenvolvedora. Isso permite delegar tarefas repetitivas e acelerar o processo de desenvolvimento, liberando as pessoas desenvolvedoras para se concentrar em questões de nível mais amplo.

Você explorará os seguintes aspectos com o agente de nuvem do Copilot:

- personalizar o ambiente para gerar código;
- garantir que as operações sejam realizadas com segurança;
- a importância de issues claramente delimitadas;
- atribuir issues ao Copilot.

## Cenários

A Tailspin Toys possui alguns itens de dívida técnica que gostaria de resolver. Os contratantes contratados inicialmente para criar a primeira versão do site deixaram a documentação em estado inadequado — mais especificamente, ela está praticamente ausente. Como primeiro passo, a equipe gostaria que comentários TSDoc fossem adicionados a todas as funções exportadas do aplicativo.

Além disso, a equipe de design está pronta para melhorar a descoberta dos jogos. Ela gostaria que a página de detalhes de cada jogo mostrasse jogos relacionados — outros títulos da mesma categoria — para que as pessoas continuassem navegando. Elas não precisam de uma implementação refinada ainda; apenas querem algo utilizável para testes de aceitação da experiência do usuário. Isso é um bloqueio no momento, embora existam issues com prioridade maior.

Ambos são exemplos de tarefas que podem ser facilmente adiadas e são adequadas para serem atribuídas ao agente de nuvem do Copilot. Ele poderá trabalhar nelas de forma assíncrona, permitindo que a pessoa desenvolvedora se concentre em outras tarefas e depois revise o trabalho do Copilot e confirme se está tudo correto.

## Apresentando o agente de nuvem do GitHub Copilot

O [agente de nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) pode executar tarefas em segundo plano, como faria uma pessoa desenvolvedora. Assim como no trabalho com uma pessoa, isso pode ser feito de várias formas, inclusive [atribuindo uma issue do GitHub ao Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Depois da atribuição, o Copilot cria um pull request em rascunho para acompanhar o progresso, prepara um ambiente e começa a trabalhar na tarefa. Você pode acompanhar a sessão enquanto ela estiver em execução ou depois de concluída. Quando estiver pronta para revisão, o Copilot mencionará você no pull request.

## A importância de instruções bem delimitadas

Não há mágica no GitHub Copilot — você não pode deixar de pensar. Mesmo operações aparentemente simples podem carregar complexidade, portanto [tenha cuidado ao delimitar tarefas para o agente de nuvem do Copilot][cloud-agent-best-practices]. Trate-o como uma pessoa parceira de programação com IA: trabalhe em etapas, aprenda, experimente e adapte-se ao longo do processo. Os fundamentos do desenvolvimento de software não mudam pela inclusão de IA generativa.

## Instruções personalizadas neste repositório

Exercícios anteriores apresentaram instruções personalizadas e como elas orientam o Copilot. Se você já fez o exercício prático de instruções personalizadas, viu `.github/copilot-instructions.md` em ação. Caso contrário, este é um bom momento para dar uma rápida olhada. Antes de atribuir trabalho ao agente de nuvem do Copilot, leia somente os arquivos de instruções já incluídos no repositório para observar seus efeitos depois.

Abra os seguintes arquivos na interface web do GitHub do seu repositório ou em um codespace que já esteja em execução:

- `.github/copilot-instructions.md` - revise a seção **Code standards**, especialmente as expectativas para convenções de TypeScript e comentários TSDoc.
- `.github/instructions/unit-tests.instructions.md` - observe o frontmatter `applyTo`, que limita essas instruções aos arquivos `**/*.test.ts`.

Quando atribuir a issue `Code lacks documentation` ao agente de nuvem na próxima seção, observe no pull request resultante os comentários TSDoc, as convenções de TypeScript e os cabeçalhos de comentário; eles vêm desses arquivos de instruções.

## Configure o ambiente de desenvolvimento para o agente de nuvem

Criar código, independentemente de quem esteja envolvido, normalmente exige um ambiente específico e scripts de configuração para garantir que tudo esteja em condições adequadas. Isso também vale ao atribuir tarefas ao Copilot, que executa tarefas de forma semelhante a um engenheiro de software.

O agente de nuvem usa [GitHub Actions][github-actions] como ambiente de trabalho. Você pode personalizar esse ambiente criando um [fluxo de trabalho de configuração especial][setup-workflow] em `.github/workflows/copilot-setup-steps.yml`, que será executado antes de o agente começar:

```yaml
name: "Copilot Setup Steps"

# Permite executar o fluxo de trabalho manualmente pela aba Actions
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Concede somente as permissões necessárias
    permissions:
      # Necessário para clonar o repositório
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuração do frontend/aplicativo
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra e prepara o banco SQLite local
      - name: Set up the database
        run: npm run db:setup
```

Esse arquivo se parece com qualquer outro fluxo de trabalho do GitHub, mas tem alguns pontos importantes:

- Ele contém um único job chamado `copilot-setup-steps`. O job é executado no GitHub Actions antes o Copilot começar a trabalhar no pull request.
- O acionador `workflow_dispatch` permite executar o fluxo manualmente pela aba **Actions** do repositório.

## Adicione documentação

Embora todos compreendam a importância da documentação, muitos projetos têm informações desatualizadas ou não têm documentação alguma. Esse é o tipo de dívida técnica que frequentemente fica sem tratamento, reduzindo a produtividade e dificultando a manutenção da base de código ou a integração de novas pessoas à equipe. Felizmente, o Copilot se destaca na criação de documentação, e esta é uma issue adequada para atribuir ao agente de nuvem do Copilot. Ele trabalhará em segundo plano para gerar a documentação necessária. Em um exercício futuro, você revisará o trabalho.

1. Acesse seu repositório no github.com em uma nova aba do navegador.
2. Selecione a aba **Issues**.
3. Selecione **New issue**.
4. Selecione **Blank issue**.
5. Defina o **Title** como `Code lacks documentation`.
6. Defina a **Description** como:

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. Selecione **Create**.
8. À direita, selecione **Assign to Copilot**.

   ![Atribuindo o Copilot a uma issue](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

   ![Detalhes da atribuição ao Copilot](../../../_images/ex4-assign-copilot-details.png)

10. Selecione a aba **Pull Requests**.
11. Abra o novo pull request, cujo título será semelhante a `[WIP]: Code lacks documentation`. Se ele não aparecer, aguarde alguns minutos e atualize a página.
12. Depois de alguns minutos, o Copilot terá criado uma lista de tarefas.

> [!NOTE]
> A lista de tarefas pode levar vários minutos para aparecer no PR. O Copilot está preparando o ambiente, executando o fluxo destacado anteriormente, analisando o projeto e determinando a melhor abordagem.

13. Revise a lista e as tarefas que serão concluídas.
14. Role pela linha do tempo do pull request até ver uma atualização indicando que o Copilot começou a trabalhar na issue.
15. Selecione **View session**.

   ![Visualização da sessão do Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Talvez seja necessário atualizar a janela para ver o indicador atualizado.

16. Observe que você pode percorrer a sessão ao vivo e acompanhar a solução do problema. Isso inclui explorar o código, compreender o estado, pensar e decidir sobre o plano apropriado e criar código.

Essa tarefa pode levar vários minutos. Um dos principais objetivos do agente de nuvem do Copilot é permitir que ele execute tarefas de forma assíncrona, liberando você para outras atividades. Vamos aproveitar esse recurso atribuindo outra tarefa ao agente de nuvem e, ao mesmo tempo, criando código para adicionar funcionalidades ao aplicativo.

## Adicione uma seção de jogos relacionados à página de detalhes

Como destacado, uma grande vantagem do agente de nuvem do GitHub Copilot é a capacidade de dividir o trabalho: você pode se concentrar em um conjunto de tarefas enquanto ele trabalha em outro. Adicionar uma seção de jogos relacionados pode não levar muito tempo, mas esse tempo poderia ser usado em outras tarefas. Vamos atribuí-la ao agente de nuvem do Copilot.

1. Volte ao repositório no github.com.
2. Selecione a aba **Issues**.
3. Selecione **New issue**.
4. Selecione **Blank issue**.
5. Defina o **Title** como `Show related games on the game details page`.
6. Defina a **Description** como:

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. Selecione **Create**.
8. À direita, selecione **Assign to Copilot**.

   ![Atribuindo o Copilot a uma issue](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

Pouco depois, você verá um conjunto de 👀 no primeiro comentário da issue, indicando que o Copilot está trabalhando nela.

O Copilot agora está trabalhando diligentemente em sua segunda solicitação. O agente de nuvem do Copilot funciona de maneira semelhante a um SWE, portanto você não precisa acompanhá-lo constantemente; basta revisar o trabalho depois que ele terminar. Agora vamos nos concentrar em criar e usar agentes personalizados.

## Resumo e próximos passos

Esta lição explorou o [agente de nuvem do GitHub Copilot][copilot-agents]. Com o agente de nuvem, você pode atribuir issues ao Copilot para execução assíncrona. O Copilot pode resolver dívida técnica, criar novas funcionalidades ou migrar código de um framework para outro.

Você explorou estes conceitos:

- personalizar o ambiente para gerar código;
- garantir que as operações sejam realizadas com segurança;
- a importância de issues claramente delimitadas;
- atribuir issues ao Copilot.

Com o agente de nuvem trabalhando em segundo plano, agora podemos criar e usar agentes personalizados. [O agente de nuvem do Copilot também pode usar servidores MCP][cloud-agent-mcp] e possui instruções personalizadas disponíveis, que exploramos em módulos anteriores.

## Recursos

- [Sobre o agente de nuvem do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Boas práticas do fluxo de configuração do agente de nuvem do Copilot][cloud-agent-best-practices]

| [Próxima lição: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
