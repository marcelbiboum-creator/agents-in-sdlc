---
title: "Lição 6 - Validar a funcionalidade com o Playwright MCP"
description: "Inspecione ou configure o Playwright MCP no Copilot CLI e use-o para explorar a funcionalidade de filtragem em um navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como já destacamos, escrever código é apenas uma parte do trabalho. É necessário lidar com dados, serviços externos e até disponibilizar automações adicionais ao Copilot. É aqui que entram os servidores MCP. Eles permitem que o Copilot vá além do que está integrado à CLI e tenha acesso a mais ferramentas e serviços.

Nesta lição, você irá:

- entender o que é o Model Context Protocol (MCP) e como o Copilot CLI o utiliza.
- adicionar o servidor MCP do Playwright caso ele ainda não esteja disponível.
- pedir ao agente que controle um navegador e explore sua funcionalidade de filtragem.

## Cenário

Embora testes de unidade e testes ponta a ponta sejam importantes, validar atualizações da interface exige interagir com ela. Você deseja permitir que o Copilot use o site em que está trabalhando como um usuário faria, para automatizar ainda mais as alterações e aumentar a confiança de que elas funcionam como esperado.

## O que é o Model Context Protocol (MCP)?

O [Model Context Protocol (MCP)][mcp-blog-post] oferece aos agentes de IA uma forma de se comunicar com ferramentas e serviços externos. Ao usar MCP, os agentes podem se comunicar com essas ferramentas e serviços em tempo real. Isso permite acessar informações atualizadas e executar ações em seu nome.

Essas ferramentas e recursos são acessados por meio de um servidor MCP, que funciona como uma ponte entre o agente de IA e os serviços externos. Cada servidor MCP representa um conjunto diferente de ferramentas e recursos aos quais o agente pode acessar.

Alguns servidores MCP populares são:

- **[Servidor MCP do GitHub][github-mcp]**: fornece acesso às APIs para gerenciar repositórios, issues e pull requests do GitHub.
- **[Servidor MCP do Playwright][playwright-mcp-server]**: fornece recursos de automação de navegador usando Playwright.

Há muitos outros servidores MCP disponíveis. O GitHub mantém um [registro MCP][mcp-registry] para melhorar a descoberta e a contribuição com o ecossistema.

> [!CAUTION]
> Trate servidores MCP como qualquer outra dependência do projeto. Antes de usar um, revise seu código-fonte, confirme o editor e considere as implicações de segurança.

## Adicione o servidor MCP do Playwright

Se o servidor MCP do Playwright ainda não estiver disponível, adicione-o para que o Copilot possa interagir com o site como um usuário faria.

> [!NOTE]
> Se o Playwright MCP já estiver configurado no Copilot CLI, pule estas etapas de configuração e continue para a próxima seção.

1. Volte ao seu Codespace.
2. Abra o diálogo para adicionar um servidor MCP digitando o seguinte comando no Copilot CLI:

   ```plaintext
   /mcp add
   ```

3. Em nome, digite `playwright` e pressione <kbd>Tab</kbd>.
4. Confirme o tipo de servidor **STDIO** pressionando <kbd>Enter</kbd> e depois <kbd>Tab</kbd>.
5. Cole o seguinte no diálogo **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pressione <kbd>Control</kbd>+<kbd>S</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para salvar o novo servidor MCP.
7. Pressione <kbd>Esc</kbd> para sair do diálogo MCP.

## Peça ao Copilot que explore a funcionalidade pelo Playwright

Antes, você confirmou manualmente que a funcionalidade se comportava como esperado. Agora vamos usar o servidor MCP do Playwright disponível no Copilot para fazer o mesmo.

1. Use o seguinte prompt para pedir ao Copilot que use o servidor MCP do Playwright e valide a funcionalidade:

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> Você não precisa dizer explicitamente ao Copilot para usar o servidor MCP, pois ele normalmente descobre isso por conta própria. Mesmo assim, indicar a ferramenta certa pode ajudar a manter os resultados consistentes e economizar alguns tokens.

2. Observe enquanto o Copilot lista os passos executados no navegador para confirmar que a funcionalidade funciona.
3. Leia o relatório e verifique se tudo se comporta como esperado.

O Copilot iniciará o servidor, usará o Playwright para interagir com o site, parará o servidor e fornecerá um relatório.

## Resumo e próximos passos

Parabéns: você usou o servidor MCP do Playwright para explorar sua funcionalidade em um navegador real a partir do Copilot CLI. Em resumo, você:

- aprendeu o que é o Model Context Protocol (MCP) e como o Copilot CLI o utiliza.
- adicionou o servidor MCP do Playwright, caso ele não estivesse disponível.
- pediu ao agente que controlasse um navegador e explorasse sua funcionalidade de filtragem.

Em seguida, você [criará um agente personalizado de QA][next-lesson] que reúne a skill e as ferramentas de navegador em uma função especializada.

## Recursos

- [O que é MCP e por que todos estão falando dele?][mcp-blog-post]
- [Servidor MCP do Microsoft Playwright][playwright-mcp-server]
- [Adicionar servidores MCP ao Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
