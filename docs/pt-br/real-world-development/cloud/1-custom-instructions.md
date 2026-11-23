---
title: "Exercício 1 - Instruções personalizadas (Agente de nuvem)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Agente de nuvem do Copilot →][next-lesson]

O contexto é essencial ao trabalhar com IA generativa. Quando uma tarefa precisa ser executada de uma maneira específica — ou há informações gerais que o Copilot deve conhecer — é necessário garantir que esse contexto esteja acessível. Os [arquivos de instruções][instruction-files] são a forma de fornecer essa orientação, para que o Copilot compreenda não apenas *o que* você quer que ele faça, mas também *como* deseja que seja feito.

Neste exercício, você irá:

- explorar como o contexto específico do projeto, as diretrizes de programação e os padrões de documentação chegam ao Copilot por meio de instruções personalizadas do repositório e arquivos de instrução com escopo por caminho.
- adicionar um novo padrão válido para todo o repositório em `.github/copilot-instructions.md`.

> [!NOTE]
> Diferentemente dos percursos de VS Code e CLI, aqui você não executará um prompt de antes/depois — o agente de nuvem do Copilot trabalha de forma assíncrona em issues do GitHub, portanto o impacto é mais difícil de demonstrar lado a lado em tempo real. Você verá a influência do arquivo de instruções mais tarde neste percurso, ao revisar os pull requests produzidos pelo agente de nuvem.

## Arquivos de instruções

### Cenário

Como toda boa equipe de desenvolvimento, a Tailspin Toys tem um conjunto de diretrizes e requisitos para suas práticas de desenvolvimento. Eles incluem:

- A camada de dados sempre precisa de testes de unidade.
- A interface deve usar o modo escuro e ter uma aparência moderna.
- A documentação deve ser adicionada ao código na forma de comentários TSDoc.
- Um bloco de comentários deve ser adicionado ao início de cada arquivo para explicar o que ele faz.

Ao usar arquivos de instruções, você garantirá que o Copilot tenha as informações certas para executar as tarefas de acordo com as práticas destacadas.

### Instruções personalizadas

Instruções personalizadas permitem fornecer contexto e preferências ao Copilot, para que ele compreenda melhor seu estilo de programação e seus requisitos. Esse recurso ajuda a orientar o Copilot a produzir sugestões e trechos de código mais relevantes. Você pode especificar convenções de programação preferidas, bibliotecas e até os tipos de comentários que deseja incluir no código. É possível criar instruções para todo o repositório ou para tipos específicos de arquivo.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md`, um único arquivo de instruções enviado ao Copilot em **toda** solicitação feita ao repositório. Ele deve conter informações no nível do projeto relevantes para a maioria das solicitações de chat ou da CLI.
- `.github/instructions/*.instructions.md`, que fornece diretrizes para tarefas ou tipos de arquivo específicos.

> [!NOTE]
> Ao trabalhar no IDE, os arquivos de instruções são usados apenas para geração de código no Copilot Chat — não para preenchimento de código nem para sugestões da próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente de nuvem do Copilot usam arquivos no nível do repositório e arquivos `*.instructions.md` (com frontmatter `applyTo`) ao gerar código.
>
> Por fim, o Copilot [também oferece suporte a arquivos de instruções com outros padrões][custom-instructions-support], incluindo arquivos `AGENTS.md` e `CLAUDE.md`.

### Boas práticas para gerenciar arquivos de instruções

Uma discussão completa sobre como criar arquivos de instruções está além do escopo deste workshop. No entanto, os exemplos fornecidos no projeto de exemplo mostram uma abordagem representativa. Em alto nível:

- Mantenha as instruções em `copilot-instructions.md` focadas em orientações no nível do projeto, como uma descrição do que está sendo criado, a estrutura do projeto e os padrões globais de programação.
- Use arquivos `*.instructions.md` para fornecer instruções específicas para tipos de arquivo (testes de unidade, componentes Astro, camada de dados) ou tarefas específicas.
- Use linguagem natural. Mantenha as orientações claras e forneça exemplos de como o código deve — e não deve — ser escrito.

Não existe uma única forma correta de criar arquivos de instruções, assim como não existe uma única forma correta de usar IA. Por meio de experimentação, você descobrirá o que funciona melhor no seu projeto.

> [!TIP]
> Todo projeto que usa o GitHub Copilot deveria ter uma coleção sólida de arquivos de instruções. Ao explorar os arquivos deste projeto, você pode encontrar instruções para vários tipos de tarefa, incluindo [atualizações de UI][ui-instructions] e [Astro][astro-instructions].
>
> O Copilot também pode ajudar a gerar arquivos de instruções. Cada interface expõe esse recurso de uma forma diferente (por exemplo, **Configure Chat → Generate Agent Instructions** no VS Code ou `/init` no Copilot CLI). A lição correspondente destacará isso quando for relevante.
>
> Procura modelos ou um ponto de partida? Explore o [awesome-copilot][awesome-copilot], um repositório repleto de arquivos de instruções, agentes personalizados e outros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explore os arquivos de instruções personalizadas deste projeto

Reserve um momento para ler os arquivos de instruções fornecidos por este repositório — há um `copilot-instructions.md` principal e uma coleção de arquivos `*.instructions.md` para várias tarefas. Abra-os no editor ou na interface web do GitHub.

1. Abra `.github/copilot-instructions.md`.
2. Explore o arquivo e observe a breve descrição do projeto, além de seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Em **Code standards**, observe a orientação de **GitHub Actions Workflows**. Essas informações se aplicam a qualquer interação com o Copilot.
3. Abra a pasta `.github/instructions` e explore seu conteúdo. Observe que há instruções para arquivos Astro, para a camada de dados Drizzle, para testes e muito mais.
4. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo` no topo — ele define um glob relativo à raiz do repositório e determina a quais arquivos as instruções se aplicam.
5. Observe as instruções específicas para criar testes de unidade neste projeto.
6. Por fim, abra `.github/instructions/drizzle.instructions.md` e role até o final. Observe os links para outros arquivos de instruções e para arquivos existentes no projeto.

> [!NOTE]
> A seção **Code formatting requirements** em `copilot-instructions.md` documenta os padrões de codificação do projeto, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários TSDoc e cabeçalhos de comentário no início dos arquivos.

## Adicione um novo padrão ao repositório

O próximo passo é a única edição que você fará aqui: adicione uma regra válida para todo o projeto, determinando que a documentação viva no código como comentários TSDoc e como cabeçalho no nível do arquivo. O agente de nuvem será informado dessa regra ao trabalhar nas issues que você atribuir a ele posteriormente neste percurso.

Antes de editar, prepare uma branch:

1. No terminal do codespace, crie e mude para uma nova branch:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

Como destacado anteriormente, `.github/copilot-instructions.md` foi criado para fornecer informações no nível do projeto ao Copilot. Vamos garantir que os padrões de codificação do repositório estejam documentados para melhorar as sugestões de código.

1. Abra novamente `.github/copilot-instructions.md`.
2. Localize a seção **Code formatting requirements**, que deve estar próxima da linha 27.
3. Adicione as linhas Markdown a seguir logo abaixo dos padrões existentes para instruir o Copilot a incluir cabeçalhos de comentário no início do arquivo e comentários TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Salve `copilot-instructions.md`.

> [!TIP]
> Como você viu na lição anterior, arquivos de instruções podem ser criados no nível do repositório (`.github/copilot-instructions.md`) para orientações globais, ou como arquivos `*.instructions.md` para linguagens, tipos de arquivo ou tarefas específicas. O arquivo do repositório é o local certo para padrões válidos em todo o projeto.

## Confirme, envie e mescle a atualização das instruções

O agente de nuvem lê os arquivos de instruções da branch destinada pela issue. Quando você atribuir uma issue ao Copilot no próximo exercício, o Copilot criará a branch a partir de `main`, portanto suas alterações de instruções precisam chegar a `main` para serem reconhecidas.

1. Prepare e confirme as alterações:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envie a branch:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. Abra um pull request de `custom-instructions-cloud` para `main` em github.com e faça o merge. O agente de nuvem lerá essas instruções ao trabalhar nas issues atribuídas no próximo exercício.

> [!TIP]
> Se preferir trabalhar diretamente em `main` neste workshop, pode pular a branch e confirmar diretamente em `main`. A etapa da branch está aqui para que o workshop reflita como você lidaria com isso em um projeto real.

## Resumo e próximos passos

Você explorou como o Copilot obtém contexto dos arquivos de instruções deste projeto e adicionou um novo padrão válido para todo o repositório em `.github/copilot-instructions.md`. Você verá esse padrão aplicado nos pull requests gerados pelo agente de nuvem ao longo deste percurso.

Em seguida, você [atribuirá sua primeira issue ao agente de nuvem do Copilot][next-lesson].

## Recursos

- [Arquivos de instruções para personalização do GitHub Copilot][instruction-files]
- [Boas práticas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções personalizadas melhores para o Copilot][copilot-instructions-five-tips]
- [Awesome Copilot — uma coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
