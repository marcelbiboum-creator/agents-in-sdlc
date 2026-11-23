---
title: "Lição 1 - Instalar o GitHub Copilot CLI"
description: "Instale e autentique o Copilot CLI no Codespace, familiarize-se com ele e encontre a issue de filtragem preparada."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

O [GitHub Copilot CLI][about-copilot-cli] é um poderoso assistente de programação baseado em agentes que é executado no terminal e permite explorar bases de código, gerar código, executar comandos e interagir com ferramentas externas — tudo pela linha de comando. Ele permite delegar tarefas, solicitar alterações e manter o foco. Como você pode imaginar, o primeiro passo é instalar a ferramenta. Felizmente, isso pode ser feito com ferramentas que você já conhece.

Nesta lição, você irá:

- instalar o GitHub Copilot CLI usando npm.
- autenticar-se com sua conta do GitHub.
- confiar no repositório do workshop e experimentar uma conversa rápida.
- encontrar a issue de filtragem por meio do servidor MCP integrado do GitHub.

## Cenário

Sua equipe está começando a usar agentes de IA para avançar em um backlog crescente. O Copilot CLI leva esse recurso ao terminal, onde muitas pessoas desenvolvedoras já trabalham. Nesta lição, você fará a instalação, a autenticação e a preparação para usá-lo no restante do workshop.

## Instale o Copilot CLI

Você pode instalar o Copilot CLI por meio do [npm][install-cli], do WinGet e do Homebrew. Como o GitHub Codespaces já inclui o Node.js, você usará npm.

1. Volte ao seu Codespace e abra um terminal.
2. Confirme que o Node.js está instalado e atende ao requisito de versão:

   ```bash
   node --version
   ```

   Você deve ver a versão 24 ou superior.

3. Instale o Copilot CLI globalmente:

   ```bash
   npm install -g @github/copilot
   ```

4. Verifique a instalação:

   ```bash
   copilot --version
   ```

   Você deve ver o número da versão exibido.

## Autentique-se no GitHub

Na primeira execução, o Copilot CLI solicita que você autentique sua conta do GitHub.

1. Inicie o Copilot CLI:

   ```bash
   copilot
   ```

2. Se solicitado, siga as instruções do código de dispositivo para autenticar e autorizar o Copilot CLI.
3. O Copilot CLI exibirá o seguinte prompt:

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. Confirme que o caminho corresponde ao repositório Tailspin Toys e responda sim selecionando **Yes, and remember this folder for future sessions**.

> [!NOTE]
> Em um Codespace, você talvez já esteja autenticado pela sua sessão do GitHub. Se o Copilot CLI iniciar sem solicitar autenticação, está tudo certo.

## Familiarize-se

Comandos no prompt normal do shell são executados diretamente no Codespace. Depois que o Copilot CLI inicia, a linguagem natural é enviada ao agente e os comandos de barra controlam a conversa.

1. Digite `/model`, use as teclas de direção para selecionar **Auto**, pressione <kbd>Enter</kbd> e pressione <kbd>Enter</kbd> novamente para confirmar.
2. Digite `/help` para ver os comandos disponíveis na versão instalada e pressione <kbd>Esc</kbd> para fechar a tela de ajuda.
3. Faça uma pergunta simples ao Copilot para confirmar que tudo está funcionando:

   ```plaintext
   What are the key files in this project?
   ```

4. Leia a resposta e observe como o Copilot explora o repositório antes de responder.
5. Digite `/mcp list` e confirme que o servidor MCP integrado do GitHub está disponível.
6. Peça ao Copilot que encontre a issue de filtragem:

   ```plaintext
   Using GitHub MCP, find the issue in this repository titled "Allow users to filter games by category and publisher." Give me its URL and a short summary. Don't change anything.
   ```

7. Abra a URL e leia a issue. Você usará a issue depois de concluir uma primeira alteração rápida.

> [!TIP]
> Uma sessão normal do Copilot CLI funciona na branch que está ativa no terminal; ela não cria automaticamente um worktree. Você criará uma branch de funcionalidade antes de cada alteração.

## Use o atalho do workshop

Normalmente, o Copilot CLI solicita autorização antes de usar ferramentas fora das permissões estabelecidas. Neste workshop, você o reiniciará com `--yolo`, um atalho aprovado pelo usuário que remove esses prompts de aprovação dentro do Codespace para que você possa se concentrar nos exercícios.

> [!CAUTION]
> `--yolo` habilita permissões automáticas completas (`--allow-all-tools`, `--allow-all-paths` e `--allow-all-urls`). Use-o somente em um ambiente isolado, como um Codespace ou uma VM, e nunca o configure como padrão no desenvolvimento diário. Consulte [Permitir ou negar o uso de ferramentas][allow-all-warning] para obter detalhes.

Neste workshop, `--enable-all-github-mcp-tools` ativa as ferramentas MCP de leitura e escrita do GitHub que lições posteriores usam para trabalhar com issues e pull requests. O Codespace limita o acesso ao seu computador local, mas os recursos autenticados do GitHub continuam sendo reais. Revise as alterações antes de publicá-las ou mesclá-las.

1. Saia do Copilot CLI com `/exit`.
2. Reinicie-o na raiz do repositório:

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. Faça outra pergunta rápida ao Copilot sobre o projeto para confirmar que a conversa está funcionando e depois saia com `/exit`.

O Copilot salva as conversas automaticamente. Mais tarde, depois de alterar instruções ou adicionar um agente, você usará `copilot --resume` para retornar à mesma conversa da funcionalidade e à mesma branch.

## Resumo e próximos passos

Parabéns! Nesta lição, você:

- instalou o GitHub Copilot CLI usando npm.
- autenticou-se com sua conta do GitHub.
- confiou no repositório do workshop e tentou uma conversa rápida.
- encontrou a issue de filtragem por meio do servidor MCP integrado do GitHub.

Em seguida, você [começará sua primeira alteração focada][next-lesson] e usará o Copilot CLI para mostrar uma avaliação por estrelas nos cards dos jogos.

## Recursos

- [Instalar o GitHub Copilot CLI][install-cli]
- [Sobre o GitHub Copilot CLI][about-copilot-cli]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
