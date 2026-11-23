---
title: "Exercício 3 - Testar sua funcionalidade com o servidor MCP do Playwright"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Modo de agente][previous-lesson] · [Próxima lição: Agentes personalizados →][next-lesson]

Você criou a funcionalidade de filtragem no modo de agente. Antes de abrir um pull request, confirme que ela realmente funciona no navegador. Em vez de navegar pelo aplicativo manualmente, você conectará o **servidor MCP do Playwright** e permitirá que o Copilot controle um navegador real.

Neste exercício, você irá:

- aprender o que é o Model Context Protocol (MCP) e como servidores MCP ampliam o Copilot;
- adicionar o servidor MCP do Playwright ao workspace;
- pedir ao Copilot que use o servidor para testar a filtragem no navegador;
- publicar a branch e abrir um pull request.

## O que é o Model Context Protocol (MCP)?

O modo de agente se torna muito mais poderoso quando pode alcançar recursos fora do editor. O [Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) permite que o Copilot se comunique com ferramentas e serviços externos.

![Diagrama mostrando o modo de agente e sua interação com contexto, LLM e ferramentas, incluindo ferramentas fornecidas por servidores MCP e extensões do VS Code](../../../_images/ex1-mcp-diagram.png)

Essas ferramentas e recursos são acessados por meio de um servidor MCP, que funciona como ponte entre o agente de IA e os serviços externos. Cada servidor representa um conjunto diferente de ferramentas e recursos.

Servidores populares incluem:

- **[Servidor MCP do GitHub](https://github.com/github/github-mcp-server)**: gerencia repositórios, issues e pull requests do GitHub.
- **[Servidor MCP do Playwright](https://github.com/microsoft/playwright-mcp)**: fornece recursos de automação de navegador.

> [!CAUTION]
> Trate servidores MCP como qualquer outra dependência. Antes de usar um, revise o código-fonte, confirme o editor e considere as implicações de segurança.

## Revise a configuração MCP

O arquivo `.vscode/mcp.json` configura os servidores MCP disponíveis neste workspace.

1. Abra `.vscode/mcp.json` no codespace.
2. Você deverá ver um servidor `github` já configurado:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

Essa entrada vem do template do projeto e permite que o Copilot leia o backlog.

## Adicione o servidor MCP do Playwright

1. Em `.vscode/mcp.json`, adicione uma entrada `playwright` ao lado de `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Salve o arquivo.

Ao contrário do servidor remoto `github`, `playwright` é um servidor local. O VS Code o inicia executando `npx @playwright/mcp@latest`. A opção `--headless` faz o navegador executar sem uma janela visível.

> [!NOTE]
> O projeto Tailspin Toys já usa Playwright para testes ponta a ponta. Se o Copilot informar que falta um navegador, peça que ele execute `npx playwright install chromium`.

## Inicie e confie no servidor

O VS Code inicia servidores MCP sob demanda. Na primeira vez que o Copilot precisar de um servidor, ele perguntará se você confia nele.

1. Em `.vscode/mcp.json`, selecione **Start** acima da entrada `playwright`.
2. Se o VS Code pedir confirmação de confiança, revise a configuração e confirme.

## Teste a funcionalidade de filtragem

Com o servidor conectado e o aplicativo em execução, peça ao Copilot que teste a funcionalidade:

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

O Copilot abrirá um navegador, percorrerá os passos e apresentará um relatório.

> [!NOTE]
> O aplicativo precisa estar disponível em `http://localhost:4321`. Se o servidor tiver sido interrompido, reinicie-o antes de enviar o prompt.

## Publique a branch e crie um pull request

Agora que a funcionalidade foi confirmada, você pode abrir um PR.

1. Abra o painel **Source Control** e revise as alterações feitas pelo Copilot.
2. Prepare as alterações selecionando o ícone **+**.
3. Gere uma mensagem de commit usando o botão **Sparkle**.
4. Selecione **Publish** para enviar a branch.
5. No Copilot Chat, selecione **New Chat** e peça que ele crie o PR:

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

6. Selecione o link gerado pelo Copilot para revisar o pull request, mas não faça o merge ainda.

## Resumo e próximos passos

Neste exercício, você:

- aprendeu o que é o Model Context Protocol (MCP);
- adicionou o servidor MCP do Playwright;
- usou-o para testar a funcionalidade de filtragem em um navegador;
- publicou a branch e abriu um pull request.

Em seguida, [crie um agente personalizado][next-lesson] para agilizar tarefas específicas como revisões de acessibilidade.

## Recursos

- [Servidor MCP do Microsoft Playwright][playwright-mcp-server]
- [Servidor MCP do GitHub][github-mcp-server]
- [Servidores MCP no VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp-server]: https://github.com/github/github-mcp-server
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
