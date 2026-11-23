---
title: "Exercício 1 - Instruções personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Modo de agente →][next-lesson]

O contexto é essencial ao trabalhar com IA generativa. Quando uma tarefa precisa ser executada de uma maneira específica — ou há informações gerais que o Copilot deve conhecer — é importante disponibilizá-las. Uma das principais formas de compartilhar esse contexto são os [arquivos de instruções][instruction-files].

Neste exercício, você irá:

- explorar como o contexto específico do projeto, as diretrizes de codificação e os padrões de documentação chegam ao Copilot.
- gerar o primeiro bloco de dados para filtragem com as instruções atuais.
- adicionar um novo padrão válido para todo o repositório em `.github/copilot-instructions.md`.
- executar novamente o mesmo prompt e observar o código seguir o novo padrão.
- confirmar a atualização das instruções e o bloco de filtragem em `main`.

> [!CAUTION]
> O código gerado pode divergir de alguns padrões definidos. O Copilot não é determinístico. O objetivo é observar a tendência de mudança após a atualização das instruções.

## Arquivos de instruções

Como toda boa equipe de desenvolvimento, a Tailspin Toys tem um conjunto de diretrizes e requisitos:

- a camada de dados sempre precisa de testes de unidade;
- a interface deve usar o modo escuro e ter aparência moderna;
- a documentação deve ser adicionada ao código como comentários TSDoc;
- um bloco de comentários deve ser adicionado ao início de cada arquivo.

Há dois tipos de arquivos:

- `.github/copilot-instructions.md`, enviado ao Copilot em toda solicitação feita ao repositório;
- `.github/instructions/*.instructions.md`, que fornece diretrizes para tarefas ou tipos de arquivo específicos.

## Explore os arquivos de instruções

1. Abra `.github/copilot-instructions.md`.
2. Observe a descrição do projeto e seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**.
3. Abra a pasta `.github/instructions` e explore os arquivos para Astro, Drizzle, testes e muito mais.
4. Abra `.github/instructions/unit-tests.instructions.md` e observe o campo `applyTo`.
5. Abra `.github/instructions/drizzle.instructions.md` e observe os links para outros arquivos de instruções e arquivos existentes no projeto.

> [!NOTE]
> A seção **Code formatting requirements** ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários TSDoc e cabeçalhos de comentário no início dos arquivos.

## Crie uma branch

1. Volte ao codespace do exercício anterior.
2. Abra um novo terminal pressionando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crie e mude para uma nova branch:

   ```bash
   git checkout -b custom-instructions
   ```

## Use o Copilot Chat antes de atualizar as instruções

1. Feche abas abertas que possam fornecer contexto desnecessário.
2. Abra `src/lib/publishers.ts`.
3. Selecione **Agent** no seletor de agentes da visualização de Chat.

   ![Captura de tela mostrando o seletor de agente](../../../_images/shared-chat-mode-selector.png)

4. Envie o seguinte prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. O Copilot explorará o projeto e aplicará alterações ao código.
6. Observe que o helper sugerido recebe um cliente `db` e retorna uma matriz tipada de editoras.
7. Observe que o código não inclui comentários TSDoc nem cabeçalho no nível do arquivo.

## Adicione um novo padrão ao repositório

1. Abra novamente `.github/copilot-instructions.md`.
2. Localize **Code formatting requirements**, próximo da linha 27.
3. Adicione estas linhas:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Salve `copilot-instructions.md`.

## Execute o prompt novamente

1. Selecione **New Chat** no Copilot Chat.
2. Abra novamente `src/lib/publishers.ts`.
3. Envie o mesmo prompt usado antes.
4. Observe que o arquivo agora começa com um bloco de comentários semelhante a:

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. Observe que a função agora inclui um comentário TSDoc semelhante a:

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

## Confirme as instruções e envie a branch

1. Confirme as alterações:

   ```bash
   git status
   ```

2. Adicione e confirme:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

3. Envie a branch:

   ```bash
   git push -u origin custom-instructions
   ```

## Crie e mescle um pull request

1. Abra o Copilot Chat no codespace.
2. Pressione <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux).
3. Peça ao Copilot que encontre a issue relacionada e crie um PR a partir da branch atual.
4. Permita as ações do GitHub solicitadas pelo Copilot.
5. Depois que o PR for criado, peça ao Copilot que o mescle e retorne a branch local para `main`.

## Próximos passos

[Próxima lição: Modo de agente →][next-lesson]

## Recursos

- [Instruções personalizadas para o GitHub Copilot][instruction-files]
- [Awesome Copilot][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
