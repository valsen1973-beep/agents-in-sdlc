---
title: "Exercício 1 - Instruções personalizadas (agente de nuvem)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Agente de nuvem do Copilot →][next-lesson]

O contexto é essencial ao trabalhar com IA generativa. Se uma tarefa precisar ser feita de uma maneira específica — ou se houver informações de contexto que o Copilot deva conhecer — você precisa disponibilizar esse contexto. Os [arquivos de instruções][instruction-files] fornecem essa orientação para que o Copilot entenda não apenas *o que* você quer, mas também *como* o trabalho deve ser feito.

Neste exercício, você vai:

- explorar como o contexto do projeto, as diretrizes de programação e os padrões de documentação chegam ao Copilot por meio das instruções personalizadas do repositório e dos arquivos de instruções com escopo por caminho.
- adicionar um novo padrão válido para todo o repositório em `.github/copilot-instructions.md`.

> [!NOTE]
> Diferentemente dos percursos do VS Code e da CLI, aqui você não executará um prompt *antes e depois*. O agente de nuvem do Copilot trabalha de forma assíncrona em issues do GitHub, então é mais difícil demonstrar o impacto das instruções lado a lado, em tempo real. Você verá a influência do arquivo de instruções mais adiante neste percurso, ao revisar os pull requests gerados pelo agente.

## Arquivos de instruções

### Cenário

Como toda boa empresa de desenvolvimento, a Tailspin Toys tem diretrizes e requisitos para as práticas de desenvolvimento. Entre eles:

- A camada de dados sempre precisa de testes unitários.
- A interface do usuário deve usar o modo escuro e ter um visual moderno.
- A documentação deve ser adicionada ao código na forma de comentários TSDoc.
- Um bloco de comentários deve ser adicionado ao início de cada arquivo para descrever sua finalidade.

Com os arquivos de instruções, você garantirá que o Copilot tenha as informações necessárias para executar as tarefas de acordo com essas práticas.

### Instruções personalizadas

As instruções personalizadas permitem fornecer contexto e preferências ao Copilot para que ele entenda melhor seu estilo de programação e seus requisitos. Esse recurso permite orientar o Copilot para gerar sugestões e trechos de código mais relevantes. Você pode especificar convenções de programação, bibliotecas e até os tipos de comentários que prefere. É possível criar instruções para todo o repositório ou para tipos específicos de arquivos e tarefas.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md`, um único arquivo enviado ao Copilot em **todas** as solicitações do repositório. Ele deve conter informações sobre o projeto — contexto relevante para a maioria das solicitações feitas ao Copilot por chat ou pela CLI, como a stack de tecnologia, uma visão geral do que está sendo criado, boas práticas e outras orientações globais.
- Arquivos `.github/instructions/*.instructions.md`, que podem fornecer orientações para linguagens específicas, como TypeScript ou Astro, ou para tarefas, como criar um componente de interface ou testes unitários.

> [!NOTE]
> No IDE, os arquivos de instruções são usados apenas para gerar código no Copilot Chat, não para autocompletar nem para sugestões da próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente de nuvem do Copilot usam tanto as instruções do repositório quanto os arquivos `*.instructions.md` com frontmatter `applyTo` ao gerar código.
>
> O Copilot também oferece suporte a outros padrões de arquivos de instruções, incluindo arquivos AGENTS.md e CLAUDE.md.

### Práticas recomendadas para gerenciar arquivos de instruções

Uma discussão completa sobre como criar arquivos de instruções está além do escopo do workshop. Ainda assim, os exemplos do projeto mostram uma abordagem representativa:

- Mantenha as instruções em `copilot-instructions.md` focadas em orientações no nível do projeto, como uma descrição do que está sendo criado, a estrutura do projeto e padrões globais de programação.
- Use arquivos `*.instructions.md` para fornecer instruções específicas para tipos de arquivo, como testes unitários, componentes Astro e a camada de dados, ou para tarefas específicas.
- Use linguagem natural e mantenha as orientações claras. Inclua exemplos de como o código deve — e não deve — ser escrito.

Não existe uma única forma de criar arquivos de instruções, assim como não existe uma única forma de usar IA. Com a experimentação, você descobrirá o que funciona melhor para o projeto.

> [!TIP]
> Todo projeto que usa o GitHub Copilot deveria ter uma coleção robusta de arquivos de instruções. Ao explorar os arquivos deste projeto, talvez você encontre instruções para vários tipos de tarefas, incluindo [atualizações de interface][ui-instructions] e [Astro][astro-instructions].
>
> O Copilot também pode ajudar a gerar arquivos de instruções. Cada interface oferece essa opção de um jeito diferente — por exemplo, **Configure Chat → Generate Agent Instructions** no VS Code ou `/init` no Copilot CLI. A lição do ambiente em que você estiver destacará essa opção quando for relevante.
>
> Procura modelos ou um ponto de partida? Explore o [awesome-copilot][awesome-copilot], um repositório repleto de arquivos de instruções, agentes personalizados e outros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explorar os arquivos de instruções personalizadas deste projeto

Reserve um momento para ler os arquivos de instruções incluídos neste repositório: há um `copilot-instructions.md` principal e uma coleção de arquivos `*.instructions.md` para várias tarefas. Abra-os no editor ou na interface web do GitHub.

1. Abra `.github/copilot-instructions.md`.
2. Explore o arquivo e observe a breve descrição do projeto e seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Em **Code standards**, observe as orientações aninhadas de **GitHub Actions Workflows**. Tudo isso se aplica a qualquer interação com o Copilot.
3. Abra a pasta `.github/instructions` e explore seu conteúdo. Há instruções para arquivos Astro, para a camada de dados Drizzle, para testes e muito mais.
4. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo` no início: ele define um glob relativo à raiz do repositório. Neste caso, qualquer arquivo de teste TypeScript, como os que correspondem a `**/*.test.ts`, será incluído.
5. Observe as instruções específicas para criar testes unitários neste projeto.
6. Abra `.github/instructions/drizzle.instructions.md` e role até o final. Observe os links para outros arquivos de instruções, como `unit-tests.instructions.md`, e para arquivos existentes do projeto. Assim, você pode dividir conjuntos de instruções maiores em arquivos menores e reutilizáveis, além de indicar exemplos para o Copilot. Os caminhos são relativos ao arquivo de instruções, não à raiz do repositório.

> [!NOTE]
> A seção **Code formatting requirements** em `copilot-instructions.md` documenta os padrões de programação, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários TSDoc e cabeçalhos de comentário no nível do arquivo.

## Adicionar um novo padrão ao repositório

Esta é a única edição que você fará neste exercício: adicione uma regra válida para todo o projeto que exija documentação no código por meio de comentários TSDoc e um cabeçalho de comentário no nível do arquivo. O agente de nuvem seguirá essa regra ao trabalhar nas issues que você atribuir mais adiante.

Antes de editar, configure uma branch de trabalho. O agente de nuvem lerá as instruções da branch para a qual a issue está direcionada, mas você fará o commit das alterações de forma organizada:

1. No terminal do Codespace, crie uma branch e mude para ela:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

Como destacado anteriormente, `.github/copilot-instructions.md` fornece informações do projeto ao Copilot. Vamos documentar os padrões de programação do repositório para melhorar as sugestões de código.

1. Abra novamente `.github/copilot-instructions.md`.
2. Localize a seção **Code formatting requirements**, que deve estar perto da linha 27. Ela documenta os padrões de programação, mas ainda não tem uma regra para documentação no código.
3. Adicione as linhas Markdown a seguir logo após os padrões existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Salve `copilot-instructions.md`.

> [!TIP]
> Como você viu na lição anterior, as instruções podem ser criadas no nível do repositório, em `.github/copilot-instructions.md`, para orientações globais, ou como arquivos `*.instructions.md` para linguagens, tipos de arquivo ou tarefas específicas. O arquivo do repositório é o lugar adequado para padrões válidos para todo o projeto, como a regra de comentários de documentação que você acabou de adicionar.

## Fazer commit, push e mesclar a atualização das instruções

O agente de nuvem lê os arquivos de instruções da branch de destino da issue. Ao atribuir uma issue ao Copilot no próximo exercício, ele criará uma branch a partir de `main`. Portanto, as atualizações das instruções precisam chegar a `main` para que o agente de nuvem as use.

1. Prepare e faça commit da alteração:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envie a branch:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. No github.com, abra um pull request da branch `custom-instructions-cloud` para `main` e faça a mesclagem. O agente de nuvem lerá essas instruções quando trabalhar nas issues atribuídas no próximo exercício.

> [!TIP]
> Se preferir trabalhar diretamente em `main` neste workshop, você pode pular a etapa da branch e fazer commit diretamente em `main`. A branch foi incluída para que o workshop reflita como o trabalho seria feito em um projeto real.

## Resumo e próximos passos

Você explorou como o Copilot usa as instruções deste projeto e adicionou um novo padrão válido para todo o repositório em `.github/copilot-instructions.md`. Você verá esse padrão nos pull requests gerados pelo agente de nuvem no restante do percurso.

Em seguida, você [atribuirá sua primeira issue ao agente de nuvem do Copilot][next-lesson].

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções personalizadas melhores para o Copilot][copilot-instructions-five-tips]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
