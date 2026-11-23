---
title: "Exercício 2 - Adicionar funcionalidades com o modo de agente do Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Mesmo uma atualização simples em um aplicativo normalmente exige alterações em vários arquivos e a execução de tarefas como testes. Como pessoa desenvolvedora, seu fluxo envolve localizar os arquivos necessários, fazer alterações, executar testes, depurar, descobrir quais arquivos ficaram de fora e atualizar o código novamente.

É aqui que entra o modo de agente do Copilot.

O modo de agente foi criado para agir de forma mais autônoma no IDE. Ele se comporta como uma pessoa desenvolvedora: começa explorando a estrutura do projeto, realiza alterações coordenadas, executa tarefas como testes e corrige automaticamente erros encontrados.

> [!NOTE]
> Embora os nomes sejam semelhantes, o modo de agente e o agente de nuvem foram criados para experiências diferentes. O modo de agente trabalha no IDE para ciclos rápidos de feedback e interação. O agente de nuvem funciona de forma assíncrona como membro da equipe.

Neste exercício, você aprenderá como:

- o modo de agente do Copilot explora o projeto e identifica arquivos relevantes;
- o modo de agente implementa novas funcionalidades na interface e na camada de dados;
- revisar alterações e testes antes de mesclá-los ao código.

## Cenário

À medida que a lista de jogos cresce, você quer permitir que as pessoas filtrem por categoria e editora. Você já adicionou um helper de editoras no exercício anterior e agora concluirá o trabalho na camada de dados, na interface e nos testes com o modo de agente.

## Execute o site da Tailspin Toys

O site é uma plataforma de financiamento coletivo para jogos de tabuleiro com tema de desenvolvimento de software. Ele permite listar jogos e mostrar detalhes. É um único aplicativo Astro que renderiza páginas como HTML estático no momento da compilação. As páginas consultam diretamente um banco SQLite local usando Drizzle ORM — não há API de backend separada nem framework de interface no cliente.

1. Volte ao codespace. Você deve estar em `main`.
2. Abra um novo terminal pressionando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crie uma branch:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicie o site:

   ```bash
   npm run dev
   ```

5. Abra o endereço do servidor Astro mostrado no terminal.

> [!NOTE]
> Em um Codespace, selecionar o endereço localhost no terminal redireciona automaticamente para `https://<nome-do-codespace>-4321.app.github.dev/`.

## Explore o backlog com o Copilot

1. Selecione **Agent** no seletor de agentes da visualização de Chat.
2. Selecione um modelo disponível.
3. Pergunte ao Copilot sobre o backlog:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Selecione **Continue** para executar o comando e listar as issues.
5. Revise a lista gerada.

## Revise os arquivos de instruções

Antes de pedir ao agente que gere código, revise o arquivo de instruções que fornecerá contexto:

1. Navegue até `.github/instructions/ui.instructions.md`.
2. Observe a visão geral da arquitetura, os princípios de componentes, testabilidade e acessibilidade e os links para outros arquivos de instruções.

## Implemente a funcionalidade de filtragem

Para concluir a filtragem, serão necessárias pelo menos três atualizações:

- adicionar ou aprimorar a lógica de filtragem na camada de dados;
- adicionar ou atualizar testes;
- atualizar a página de listagem para incluir a interface de filtragem.

1. Continue na conversa atual ou selecione **New Chat**.
2. Selecione **Add Context**, **Instructions** e o arquivo `ui`.
3. Confirme que **Agent** está selecionado.
4. Peça ao Copilot que implemente a funcionalidade:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

5. Observe enquanto o Copilot explora o projeto, localiza os arquivos, modifica o código e executa testes.
6. Se solicitado, selecione **Continue** para executar os testes.
7. Explore o código gerado e procure problemas.

> [!CAUTION]
> Sempre revise o código gerado por ferramentas de IA.

8. Volte ao navegador e teste a nova funcionalidade.
9. Quando estiver tudo correto e o código tiver sido revisado, selecione **Keep** no Copilot Chat.

## Resumo e próximos passos

Parabéns! Neste exercício, você explorou como usar o modo de agente do GitHub Copilot para adicionar funcionalidades ao site da Tailspin Toys:

- o modo de agente implementou alterações na interface e na camada de dados;
- o agente explorou o projeto, identificou arquivos relevantes e fez alterações coordenadas;
- você revisou alterações e testes antes de mesclá-los ao código.

Agora [teste sua funcionalidade com o servidor MCP do Playwright][next-lesson] e abra um pull request.

## Recursos

- [Modos ask, edit e agent do Copilot][choose-mode]
- [Modo de agente no VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
