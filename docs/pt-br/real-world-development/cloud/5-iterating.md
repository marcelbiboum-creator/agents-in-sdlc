---
title: "Exercício 5: Iterar sobre o trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

## Revisando o trabalho

Ao longo deste laboratório, você trabalhou com o GitHub Copilot em várias tarefas voltadas à melhoria da experiência do usuário e à inclusão de funcionalidades. Você pediu ao Copilot que adicionasse documentação ao código, criasse uma funcionalidade de jogos relacionados para a equipe de design iterar e implementasse funcionalidades de acessibilidade, incluindo alternâncias de modo de alto contraste e modo claro. Vamos explorar as alterações de código e, se necessário, fornecer comentários ao Copilot para melhorar seu trabalho.

### Cenário

Como destacado várias vezes, os fundamentos do design de software e de DevOps não mudam com a inclusão de IA generativa. Sempre devemos revisar o código gerado e seguir nosso processo normal de DevOps. Com isso em mente, vamos revisar as sugestões do GitHub Copilot para criação da documentação, da funcionalidade de jogos relacionados e das funcionalidades de acessibilidade antes de ativar a revisão para o restante da equipe.

## Segurança e agente de nuvem do GitHub Copilot

Como o agente de nuvem do Copilot executa tarefas de forma assíncrona e sem supervisão, certas restrições de segurança foram aplicadas:

- O Copilot tem acesso somente de leitura ao repositório e acesso de escrita apenas à branch que usará para o código.
- O agente de nuvem é executado dentro do GitHub Actions, criando um ambiente separado e temporário.
- Qualquer fluxo de trabalho do GitHub Actions exige aprovação de uma pessoa antes da execução.
- [O acesso a recursos externos é limitado por padrão][agent-firewall], incluindo servidores MCP.

## Revise a documentação gerada

Vamos começar explorando o primeiro pull request (PR) gerado pelo agente de nuvem do GitHub Copilot: a adição de documentação ao código. Você realizará esta tarefa pela interface padrão de PR no GitHub.com.

> [!NOTE]
> Ao explorar o PR, talvez veja um aviso de que o GitHub Copilot foi bloqueado por um firewall. Isso é **esperado**, pois o Copilot tem acesso limitado a recursos externos por padrão, incluindo servidores MCP externos. Se quiser, você pode [personalizar ou desativar o firewall do agente de nuvem][agent-firewall].

1. Volte ao seu repositório no github.com.
2. Selecione **Pull Requests**.
3. Abra o pull request com título semelhante a **Add missing documentation**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando na tarefa, o pull request mostrará a marca **[WIP]**. Nesse caso, aguarde alguns minutos e atualize.

4. Quando o PR estiver pronto, selecione a aba **Files changed** e revise as alterações.

   ![Aba Files changed](../../../_images/shared-pr-files-changed.png)

5. Explore o código atualizado, que inclui comentários TSDoc e outras documentações. As alterações exatas podem variar.
6. Conforme você revisa, procure comentários TSDoc, convenções de TypeScript e cabeçalhos de comentário provenientes dos arquivos de instruções personalizados.
7. Depois da revisão, volte à aba **Conversation** e role até a parte inferior.
8. Você deverá ver um indicador de alguns fluxos de trabalho aguardando aprovação.
9. Se houver fluxos aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos de trabalho](../../../_images/shared-approve-workflows.png)

10. Os fluxos serão colocados na fila na seção de verificações do PR. Se tudo estiver correto, as verificações do projeto deverão passar para o aplicativo Astro único.

## Solicite alterações ao GitHub Copilot

Trabalhar com o Copilot em um pull request não é necessariamente uma via de mão única. Você também pode mencionar o Copilot em comentários — como faria com outras pessoas da equipe — no PR ou em comentários incorporados ao código. O Copilot verá esses comentários e iniciará outra sessão para tratá-los. Como os resultados são não determinísticos, não podemos fornecer um texto prescritivo. Algumas ideias:

- Adicionar cabeçalhos de comentário no início de cada arquivo de código.
- Adicionar comentários TSDoc a arquivos TypeScript e Astro.
- Criar um README descrevendo a estrutura do aplicativo Astro.

1. Adicione um comentário solicitando uma alteração na documentação gerada e mencione **@copilot**, como faria com qualquer usuário.
2. Selecione **View Session** para acompanhar o trabalho do Copilot.
3. Selecione **Back to pull request** para retornar ao PR.

   ![Voltar ao pull request](../../../_images/ex7-back-to-pr.png)

4. Quando o Copilot concluir as alterações, haverá um novo commit no PR.
5. Selecione **Files changed** para revisar as alterações.

Continue iterando até ficar satisfeito. Depois, converta o PR de rascunho para pronto e faça o merge na branch principal.

![Converter PR para pronto](../../../_images/ex7-ready-for-review.png)

## Revise a funcionalidade de jogos relacionados

Vamos voltar ao PR criado pelo Copilot para a issue que mostrava jogos relacionados na página de detalhes.

1. Volte ao repositório no GitHub.com.
2. Selecione a aba **Pull Requests**.
3. Selecione o PR com título semelhante a **Show related games on the game details page**.
4. Selecione **Files changed** e revise o código gerado.
5. Depois da revisão, volte à aba **Conversation**.
6. Se houver indicadores de fluxos aguardando aprovação, selecione **Approve and run workflows**.
7. Confirme que as verificações passam para o aplicativo Astro.
8. **Opcional:** alterne para a branch criada pelo Copilot no Codespace e teste manualmente a funcionalidade:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

O Copilot criou a funcionalidade de jogos relacionados. Como antes, você pode iterar com o agente de nuvem solicitando ajustes, por exemplo, alterar a quantidade de jogos exibidos ou garantir cabeçalhos de comentário e comentários TSDoc.

## Revise as funcionalidades de acessibilidade

Por fim, revise as funcionalidades de acessibilidade implementadas pelo agente personalizado de acessibilidade. Este PR deve incluir tanto o modo de alto contraste quanto o modo claro solicitado no Mission control.

1. Volte ao repositório no GitHub.com.
2. Selecione a aba **Pull Requests**.
3. Abra o PR com título semelhante a **Add high contrast mode to website**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando, o PR terá a marca **[WIP]**.

4. Selecione **Files changed** e revise o código gerado.
5. Revise a implementação, especialmente:
   - os componentes de alternância entre modos;
   - o uso de armazenamento local para persistir preferências;
   - as alterações de CSS para os modos de alto contraste e claro;
   - atributos de acessibilidade (rótulos ARIA, navegação por teclado etc.);
   - código JavaScript/TypeScript que gerencia a troca de modos.

6. Volte à aba **Conversation** e aprove os fluxos de trabalho pendentes.
7. Confirme que as verificações do aplicativo Astro passam.
8. **Opcional:** alterne para a branch no Codespace e teste manualmente os modos:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Depois, inicie o aplicativo e teste os alternadores de alto contraste e modo claro no navegador, confirmando que funcionam e persistem após recarregar a página.

Observe como o agente personalizado de acessibilidade ajudou a orientar o Copilot a implementar essas funcionalidades seguindo boas práticas de acessibilidade. Se encontrar qualquer questão de acessibilidade, mencione **@copilot** em um comentário para solicitar atualizações.

## Exercício opcional — continue delegando

O agente de nuvem funciona melhor quando você entrega a ele itens reais do backlog e direciona sua atenção para outro lugar. Para criar esse hábito, registre mais algumas issues no repositório e atribua-as ao Copilot. Algumas ideias:

- criar um formulário de interesse de apoiador na página de detalhes do jogo;
- implementar paginação na lista de jogos;
- adicionar validação de entrada e tratamento de erros aos helpers da camada de dados.

## Resumo

Você concluiu o percurso do agente de nuvem. Ao longo destas lições, você:

- **inspecionou os arquivos de instruções personalizados fornecidos por este repositório**;
- **atribuiu issues ao agente de nuvem do Copilot** e acompanhou a preparação do ambiente, o planejamento e a execução assíncrona;
- **criou e usou um agente personalizado** para acessibilidade;
- **usou a página de agentes do Copilot como Mission control** para monitorar e orientar a sessão;
- **reviu e iterou sobre os pull requests**, usando `@copilot` para solicitar alterações e aprovando fluxos de trabalho.

## Revisão e próximos passos

Você concluiu o percurso do agente de nuvem. Se quiser continuar explorando, os outros percursos complementam o que você praticou aqui:

- **[Percurso do VS Code](../../vscode/)** — explore o modo de agente do Copilot Chat e a integração MCP diretamente no IDE.
- **[Percurso da CLI](../../cli/)** — entregue duas alterações revisadas pelo terminal usando os modos Plan e Autopilot, skills de agente, um agente personalizado de QA, Playwright MCP, Agent Merge e uma ponte opcional `/delegate` para o agente de nuvem.

Em seu próprio repositório, experimente estas ideias:

- atribuir uma issue de refatoração ou cobertura de testes ao agente de nuvem;
- criar um agente personalizado para outra área;
- configurar `copilot-setup-steps.yml` para outra stack.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre agentes do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Boas práticas do fluxo de configuração do agente de nuvem][cloud-agent-best-practices]
- [Configurar o firewall do agente de nuvem][agent-firewall]

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
