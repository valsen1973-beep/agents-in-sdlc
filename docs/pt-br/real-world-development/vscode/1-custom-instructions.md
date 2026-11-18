---
title: "Exercício 1 - Instruções personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Modo de agente →][next-lesson]

O contexto é essencial ao trabalhar com IA generativa. Se uma tarefa precisar ser feita de uma maneira específica — ou se houver informações de contexto que o Copilot deva conhecer — você precisa disponibilizar esse contexto. Há várias formas de fornecer contexto específico ao Copilot. Uma das principais são os [arquivos de instruções][instruction-files], que fornecem orientação sobre a geração de código.

Neste exercício, você vai:

- explorar como o contexto do projeto, as diretrizes de programação e os padrões de documentação chegam ao Copilot por meio das instruções personalizadas do repositório e dos arquivos de instruções com escopo por caminho.
- gerar a primeira parte dos dados de filtragem — um helper de editoras — usando as instruções *atuais*.
- adicionar um novo padrão válido para todo o repositório em `.github/copilot-instructions.md`.
- executar o mesmo prompt novamente e observar o código gerado adotar o novo padrão.
- fazer commit das atualizações das instruções e da primeira parte do recurso de filtragem em `main` para que o Copilot use as orientações atualizadas no próximo exercício.

> [!CAUTION]
> O código gerado pode não seguir alguns dos padrões definidos. O Copilot é não determinístico. O objetivo deste exercício é observar a *tendência* de mudança no comportamento após a atualização das instruções, não obter uma saída idêntica caractere por caractere.

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

## Criar uma branch para as alterações

Vamos seguir boas práticas e criar uma branch para as alterações.

1. Volte ao Codespace usado no exercício anterior.
2. Abra um novo terminal pressionando <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Crie uma branch e mude para ela:

   ```bash
   git checkout -b custom-instructions
   ```

## Usar o Copilot Chat *antes* de atualizar as instruções

> [!TIP]
> **Abrir o Copilot Chat**
>
> Antes de começar os exercícios abaixo, volte ao Codespace, abra o painel do Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo variam por exercício; cada etapa informa o que selecionar quando necessário.

Para observar o impacto das instruções personalizadas, comece enviando um prompt com o arquivo de instruções atual. Depois, atualize-o e envie o mesmo prompt novamente.

1. Feche as guias do editor abertas nos exercícios anteriores para que o Copilot use apenas o contexto desejado.
2. Abra `src/lib/publishers.ts` para indicar ao Copilot onde o helper deve ficar.
3. Na lista de agentes da visualização Chat, selecione **Agent** para que o Copilot possa alterar arquivos.

   ![Captura de tela do seletor de agentes na visualização Chat.](../../../_images/shared-chat-mode-selector.png)

4. Envie o prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. O Copilot explorará o projeto e aplicará atualizações no código, geralmente ao helper e aos testes.
6. Observe que o helper proposto é uma função tipada que recebe um cliente `db` como primeiro argumento e retorna um array tipado de editoras. Essa abordagem vem das convenções da camada de dados em `.github/instructions/drizzle.instructions.md`, que se aplica a `src/lib/*.ts`.
7. Observe que o código proposto **não tem** comentários TSDoc nem cabeçalho de comentário no nível do arquivo.

> [!CAUTION]
> Como o Copilot é não determinístico, talvez ele adicione comentários de documentação mesmo sem essa orientação. Se isso acontecer, tudo bem: o objetivo continua sendo observar o ganho de *consistência* depois da atualização das instruções.

## Adicionar um novo padrão ao repositório

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

## Executar o prompt novamente e observar a alteração

1. Volte ao Copilot Chat e selecione **New Chat** para limpar o contexto.
2. Clique em `src/lib/publishers.ts` para direcionar o Copilot ao arquivo correto.
3. Envie o **mesmo prompt** de antes:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. Observe que o arquivo proposto agora começa com um bloco de comentários semelhante a este:

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. Observe que a função proposta agora inclui um comentário TSDoc semelhante a este:

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

Você acabou de orientar o Copilot a seguir um novo padrão do projeto e aplicá-lo ao código que servirá de base para o próximo exercício.

## Fazer commit das instruções e enviar a branch

Os arquivos de instruções são gerenciados pelo controle do código-fonte como qualquer outro arquivo. Vamos fazer commit e enviar a branch.

1. Abra uma nova janela de terminal pressionando <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
2. Confirme se as atualizações das instruções e do helper estão presentes:

   ```bash
   git status
   ```

3. Adicione e faça commit da atualização das instruções e de todos os arquivos alterados pelo Copilot para criar a base do helper:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Se git status mostrar outras atualizações de suporte (por exemplo, testes), adicione esses arquivos também.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Envie a branch para o repositório:

   ```bash
   git push -u origin custom-instructions
   ```

## Criar e mesclar um pull request

Com a branch enviada, vamos criar um pull request e vinculá-lo à issue de padrões de documentação do backlog. Em vez de fazer isso manualmente, podemos pedir ao Copilot que encontre a issue, crie um PR para fechá-la e faça a mesclagem.

> [!NOTE]
> Este é o primeiro exercício em que o Copilot executará ações no GitHub. O modelo do projeto já conecta as ferramentas do GitHub ao ambiente, então não é preciso configurar nada. Na primeira vez que usar uma ferramenta do GitHub, talvez o VS Code peça que você entre na sua conta. Siga as instruções para permitir o acesso. Você aprenderá como essa conexão funciona — pelo Model Context Protocol — em um exercício posterior.

1. Abra o Copilot Chat no Codespace.
2. Pressione <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir a visualização Copilot Chat e confirme que **Agent** está selecionado na lista de agentes.
3. Peça ao Copilot que encontre a issue sobre a atualização do arquivo de instruções e crie um PR a partir da branch atual, descrevendo também a base do helper de editoras:

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. O Copilot começará a procurar a issue e criar o PR.
5. Quando solicitado a permitir que o Copilot execute ações do GitHub, revise o comando e selecione **Allow** se for apropriado.
6. Quando o PR for criado, peça ao Copilot que o mescle e retorne à branch main:

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. Quando solicitado a permitir que o Copilot execute ações do GitHub e comandos de shell, revise o comando e selecione **Allow** se for apropriado.

Você acaba de criar e mesclar um pull request com a ajuda do GitHub Copilot.

## Resumo e próximos passos

Você explorou como o Copilot usa as instruções deste projeto e, em seguida, usou o Copilot Chat no VS Code para:

- enviar um prompt de geração de código e observar o resultado com as instruções *existentes*.
- adicionar um novo padrão válido para todo o repositório em `.github/copilot-instructions.md`.
- executar o mesmo prompt novamente e observar o código proposto adotar o novo padrão.
- fazer commit das instruções e da base do helper em `main` para que o próximo exercício possa aproveitá-las.

Em seguida, você usará as instruções atualizadas no [modo de agente][next-lesson] enquanto o Copilot adiciona um recurso em vários arquivos.

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções personalizadas melhores para o Copilot][copilot-instructions-five-tips]
- [Instruções pessoais personalizadas para o GitHub Copilot][personal-instructions]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
