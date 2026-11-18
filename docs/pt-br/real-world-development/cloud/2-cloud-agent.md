---
title: "Exercício 2 - Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Instruções personalizadas][previous-lesson] |
|:--|

É provável que poucas organizações — se alguma — não tenham dificuldades com dívida técnica. Ela pode incluir problemas de segurança não resolvidos, código legado que precisa de atualizações ou solicitações de funcionalidades que ficaram no backlog por falta de tempo para implementá-las. O agente de nuvem do GitHub Copilot foi desenvolvido para tarefas como atualizar código e adicionar funcionalidades de forma autônoma. Quando termina o trabalho, ele cria um PR de rascunho para que uma pessoa desenvolvedora o revise. Isso permite delegar tarefas repetitivas, acelerar o desenvolvimento e liberar as pessoas desenvolvedoras para se concentrarem em questões mais amplas.

Neste exercício, você explorará o agente de nuvem do Copilot para:

- personalizar o ambiente usado para gerar código.
- garantir que as operações sejam executadas com segurança.
- entender a importância de issues bem delimitadas.
- atribuir issues ao Copilot.

## Cenários

A Tailspin Toys tem algumas dívidas técnicas para resolver. As pessoas contratadas para criar a primeira versão do site deixaram a documentação em um estado inadequado: ela está completamente ausente. Como primeiro passo, a equipe quer adicionar comentários TSDoc a todas as funções exportadas do aplicativo.

Além disso, a equipe de design quer melhorar a descoberta de jogos. Ela quer que a página de detalhes de cada jogo mostre jogos relacionados — outros títulos da mesma categoria — para que as pessoas possam continuar explorando. Por enquanto, não é necessária uma implementação refinada; basta algo que permita testar a experiência de usuário. Essa tarefa está bloqueada, mas há outras issues de prioridade maior.

Esses são exemplos de tarefas que podem ser adiadas e que são ideais para o agente de nuvem do Copilot. Ele pode trabalhar nelas de forma assíncrona enquanto a pessoa desenvolvedora cuida de outras tarefas e, depois, retorna para revisar o trabalho.

## Apresentação do agente de nuvem do GitHub Copilot

O [agente de nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) pode executar tarefas em segundo plano de forma semelhante a uma pessoa desenvolvedora. Assim como no trabalho com uma pessoa da equipe, há várias maneiras de atribuir tarefas, incluindo [atribuir uma issue do GitHub ao Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Depois de receber a atribuição, o Copilot cria um pull request de rascunho para acompanhar o progresso, configura um ambiente e começa a trabalhar. Você pode acompanhar a sessão durante a execução ou depois da conclusão. Quando a solução estiver pronta para revisão, o Copilot marcará você no pull request.

## A importância de instruções bem delimitadas

Não há mágica no GitHub Copilot — não é possível pular a etapa de raciocínio. Mesmo tarefas aparentemente simples podem se tornar complexas quando examinadas de perto. Por isso, [defina o escopo das tarefas do agente de nuvem com cuidado][cloud-agent-best-practices]. Trate-o como um assistente de programação com IA: trabalhe por etapas, aprenda, experimente e adapte o processo. Os fundamentos do desenvolvimento de software não mudam com a chegada da IA generativa.

## Instruções personalizadas neste repositório

Nos exercícios anteriores, você conheceu as instruções personalizadas e como elas orientam o Copilot. Se já concluiu o exercício prático sobre instruções personalizadas, viu `.github/copilot-instructions.md` em ação; se ainda não o fez, aproveite para examiná-lo. Antes de atribuir tarefas ao agente de nuvem, leia os arquivos de instruções já incluídos no repositório, sem alterá-los, para depois identificar seus efeitos.

Abra os arquivos a seguir na interface web do GitHub ou em um Codespace que já esteja em execução:

- `.github/copilot-instructions.md` — revise a seção **Code standards**, especialmente as expectativas sobre convenções de TypeScript e comentários TSDoc.
- `.github/instructions/unit-tests.instructions.md` — observe o frontmatter `applyTo`, que aplica as instruções aos arquivos `**/*.test.ts`.

Ao atribuir a issue `Code lacks documentation` ao agente de nuvem na próxima seção, observe no pull request os comentários TSDoc, as convenções de TypeScript e os cabeçalhos de comentário. Essas orientações vêm dos arquivos de instruções. Voltaremos a esse assunto ao revisar PRs em um exercício posterior.

## Configurar o ambiente de desenvolvimento do agente de nuvem

Normalmente, criar código exige um ambiente específico e a execução de scripts de configuração para garantir que tudo esteja em boas condições. Isso também se aplica às tarefas atribuídas ao Copilot, que trabalha de forma semelhante a uma pessoa engenheira de software.

O agente de nuvem usa o [GitHub Actions][github-actions] como ambiente de trabalho. Você pode personalizar esse ambiente criando um [workflow de configuração especial][setup-workflow] no arquivo `.github/workflows/copilot-setup-steps.yml`, executado antes do início do trabalho. Assim, o agente tem acesso às ferramentas e dependências necessárias. O arquivo já foi configurado para este laboratório: ele disponibiliza Node.js, dependências do projeto, binários de navegador para testes de ponta a ponta e o banco de dados SQLite migrado e preenchido do aplicativo Astro:

```yaml
name: "Copilot Setup Steps"

# Permite testar as etapas de configuração na guia "Actions" do repositório
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Defina as permissões no menor nível necessário para *suas etapas*. O Copilot receberá um token próprio para as operações dele.
    permissions:
      # Para clonar o repositório nas etapas de configuração, por exemplo, para instalar dependências, você precisará da permissão `contents: read`. Se não clonar o repositório nessas etapas, o Copilot fará isso automaticamente depois que elas forem concluídas.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuração do frontend/aplicativo - Node.js (todo o aplicativo agora usa Astro + Drizzle/libSQL)
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

      # Migre e preencha o banco de dados SQLite local para que o build e os testes tenham dados.
      - name: Set up the database
        run: npm run db:setup
```

O arquivo se parece com qualquer outro workflow do GitHub, mas tem alguns detalhes importantes:

- Ele contém um único job chamado `copilot-setup-steps`, executado no GitHub Actions antes de o Copilot começar a trabalhar no pull request.
- O gatilho `workflow_dispatch` permite executar o workflow manualmente na guia **Actions** do repositório. Isso é útil para testar se ele funciona, sem esperar que o Copilot o execute.

## Adicionar documentação

Embora todo mundo reconheça a importância da documentação, muitos projetos têm informações desatualizadas ou não têm documentação. Esse tipo de dívida técnica costuma ficar sem solução, reduzindo a produtividade e dificultando a manutenção da base de código e a integração de pessoas desenvolvedoras. O Copilot é particularmente útil para criar documentação, por isso esta é uma issue adequada para atribuir ao agente de nuvem. Ele trabalhará em segundo plano para gerar a documentação necessária. Em um exercício futuro, você voltará para revisar o resultado.

1. Em uma nova guia do navegador, acesse seu repositório no github.com.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue** para criar uma issue em branco.
5. Defina **Title** como `Code lacks documentation`.
6. Defina **Description** como:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecione **Create** para criar a issue.
8. No lado direito, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.

    ![Atribuição do Copilot a uma issue](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.
10. Selecione a guia **Pull Requests**.
11. Abra o pull request (PR) recém-criado, com um título semelhante a `[WIP]: Code lacks documentation`. Se o PR ainda não aparecer na lista, aguarde um ou dois minutos e atualize a página.
12. Depois de alguns minutos, o Copilot deverá criar uma lista de tarefas.

> [!NOTE]
> A lista de tarefas pode levar alguns minutos para aparecer no PR. O Copilot está configurando o ambiente com o workflow descrito acima, analisando o projeto e definindo uma abordagem para a tarefa.

13. Revise a lista e as tarefas que serão executadas.
14. Percorra a linha do tempo do pull request e procure uma atualização indicando que o Copilot começou a trabalhar na issue.
15. Selecione **View session**.

    ![Visualização da sessão do Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Talvez seja necessário atualizar a janela para ver o indicador atualizado.

16. Observe que você pode percorrer a sessão ao vivo e acompanhar como o Copilot resolve o problema: ele explora o código e entende o estado atual, pausa para pensar e definir um plano e cria código.

Isso provavelmente levará alguns minutos. Um dos objetivos principais do agente de nuvem do Copilot é executar tarefas de forma assíncrona para que você possa se concentrar em outras atividades. Vamos aproveitar esse recurso atribuindo outra tarefa ao agente e, em seguida, voltando nossa atenção para a criação de funcionalidades no aplicativo.

## Adicionar uma seção de jogos relacionados à página de detalhes

Uma das principais vantagens do agente de nuvem é dividir o trabalho: enquanto você se concentra em um conjunto de tarefas, ele cuida de outro. Mesmo que a seção de jogos relacionados para a equipe de design não leve muito tempo, esse tempo poderia ser usado em outras tarefas. Vamos atribuí-la ao agente de nuvem do Copilot.

1. Volte ao repositório no github.com.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue** para usar o modelo em branco.
5. Defina **Title** como `Show related games on the game details page`.
6. Defina **Description** como:

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. Selecione **Create** para criar a issue.
8. No lado direito, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.

    ![Atribuição do Copilot a uma issue](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

Pouco depois, você deverá ver um conjunto de 👀 no primeiro comentário da issue, indicando que o Copilot está trabalhando nela.

![O Copilot usa o emoji de olhos para indicar que está trabalhando na issue](../../../_images/ex4-issue-eyes-emoji.png)

O Copilot agora está trabalhando na segunda solicitação. O agente de nuvem funciona de forma semelhante a uma pessoa engenheira de software: você não precisa acompanhá-lo ativamente, basta revisar o resultado quando estiver pronto. Agora, vamos criar e usar agentes personalizados.

## Resumo e próximos passos

Este exercício apresentou o [agente de nuvem do GitHub Copilot][copilot-agents]. Com ele, você pode atribuir issues ao Copilot para execução assíncrona. Ele pode resolver dívidas técnicas, criar funcionalidades ou ajudar a migrar código entre frameworks.

Você explorou estes conceitos:

- personalizar o ambiente usado para gerar código.
- garantir que as operações sejam executadas com segurança.
- entender a importância de issues bem delimitadas.
- atribuir issues ao Copilot.

Enquanto o agente de nuvem trabalha em segundo plano, vamos criar e usar agentes personalizados. O [agente de nuvem também pode usar servidores MCP][cloud-agent-mcp] e tem acesso a instruções personalizadas, que já exploramos em módulos anteriores.

## Recursos

- [Sobre o agente de nuvem do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o workflow de configuração do agente de nuvem][cloud-agent-best-practices]

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
