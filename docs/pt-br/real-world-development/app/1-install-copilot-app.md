---
title: "Lição 1 - Instalar o aplicativo GitHub Copilot"
description: "Instale o aplicativo GitHub Copilot, conecte o repositório criado a partir do modelo, conheça o espaço de trabalho e experimente um chat rápido."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

O **[aplicativo GitHub Copilot][about-copilot-app]** é um aplicativo para desktop voltado ao desenvolvimento orientado por agentes. Ele é baseado no GitHub Copilot CLI e se integra nativamente ao GitHub, para que repositórios, branches e pipelines de CI funcionem desde o início. O aplicativo foi criado para fluxos de trabalho em que você orienta vários agentes em paralelo — cada um em seu próprio espaço de trabalho isolado — em vez de fazer todo o trabalho sozinho, além de automatizar tarefas repetitivas. Com o Node.js instalado e sua cópia do projeto pronta, o próximo passo é instalar o aplicativo e conectar o repositório.

Nesta lição, você vai:

- instalar o aplicativo GitHub Copilot e entrar na sua conta.
- adicionar seu projeto ao aplicativo a partir do repositório do GitHub.
- conhecer o espaço de trabalho, incluindo o backlog criado pelo modelo.
- experimentar um chat rápido para saber mais sobre o aplicativo.

## Cenário

Sua equipe está adotando agentes de IA para avançar em um backlog crescente. O aplicativo Copilot oferece um único lugar para orientar esse trabalho: selecionar issues, executar agentes, revisar alterações e mesclar pull requests. Nesta lição, você instalará e conectará o aplicativo e aprenderá a iniciar uma conversa sobre o projeto.

> [!NOTE]
> É necessário ter um plano elegível do Copilot: Copilot Free, Copilot Student ou qualquer plano pago (Pro, Pro+, Business ou Enterprise). Se você usa o Copilot Business ou o Copilot Enterprise, o administrador precisa manter habilitada a política **GitHub Copilot app**.

## Instalar e configurar o aplicativo GitHub Copilot

Para usar o aplicativo GitHub Copilot, primeiro instale-o. Há versões para Windows, macOS e Linux. Vamos instalar o aplicativo, autenticar e adicionar o repositório Tailspin Toys.

1. No navegador, abra a [página inicial do aplicativo GitHub Copilot][download-app].
2. Baixe o aplicativo para sua plataforma e instale-o seguindo as instruções da página.
3. Depois da instalação, abra o aplicativo.
4. Selecione **Sign in to GitHub** e siga as instruções para entrar com uma conta do GitHub.com ou do GHE.com. Se usar o GitHub Enterprise Cloud com residência de dados, selecione **GitHub Enterprise Cloud** e digite o nome de host `*.ghe.com` quando solicitado.

   Se usar o GitHub Enterprise Server, conclua primeiro a integração com sua conta na nuvem. Em seguida, abra **Settings**, selecione **Accounts**, selecione **Add account** e escolha **GitHub Enterprise Server**. Siga as instruções para autorizar o aplicativo no navegador, conforme descrito no [guia de entrada do Enterprise Server][ghes-sign-in].

5. Se o processo inicial oferecer a seleção de repositórios, selecione o repositório Tailspin Toys criado a partir do modelo. Você também pode pular essa etapa e adicionar o projeto depois.
6. Quando solicitado, escolha um tema e conclua a configuração inicial.
7. Procure seu repositório em **Sessions**, na barra lateral. Se ele já estiver listado, não é necessário adicioná-lo novamente.
8. Se o repositório ainda não estiver conectado, selecione **+** ao lado de **Sessions** para criar uma sessão e, em seguida, selecione **Add GitHub repository**. Use o nome do proprietário e do repositório anotados na lição de pré-requisitos.
9. Confirme que o repositório aparece na barra lateral. Neste layout, pastas de repositório como `tailspin-toys` aparecem agrupadas em **Sessions**, com as sessões individuais abaixo de cada repositório.

## Conhecer o espaço de trabalho

Com o projeto conectado, conheça o aplicativo. A barra lateral organiza o trabalho em algumas áreas:

- **New** — inicie uma nova sessão de chat com o Copilot.
- **Pull requests** — acesse seus pull requests pela integração nativa com o GitHub. Você pode navegar e filtrar PRs, consultar o estado da CI e revisar pull requests sem sair do aplicativo.
- **Issues** — acesse suas issues da mesma forma. Você pode navegar e filtrar issues e iniciar uma sessão a partir de uma issue.
- **Automations** — tarefas salvas de agentes que são executadas conforme um cronograma ou sob demanda. Elas ajudam a gerenciar listas de tarefas, manutenção periódica do projeto e outras atividades repetitivas. O resumo faz referência a elas como um próximo passo, não como outro exercício do workshop.
- **Customize** — adicione recursos ao aplicativo Copilot, como servidores MCP, plugins, skills e outros componentes. Você usará esta área para configurar o Playwright MCP.
- **Chats** — conversas rápidas para perguntas e ideias que não precisam de uma branch nem de um espaço de trabalho próprio. Essa seção aparece depois que você inicia o primeiro chat. Se não estiver visível, selecione **+** ao lado de **Sessions** para iniciar seu primeiro chat.
- **Sessions** — agrupe pastas de repositórios e as sessões de agente correspondentes. Selecione um repositório, como `tailspin-toys`, para abrir a visualização dele, ou selecione uma sessão para retomar a conversa. Cada sessão é executada em um espaço de trabalho isolado, para que você possa executar várias ao mesmo tempo sem conflito entre as alterações. Você iniciará sua primeira sessão ao adicionar classificações por estrelas.

Ao longo do workshop, você explorará o espaço de trabalho.

> [!TIP]
> Em caso de dúvida, pergunte ao Copilot. Se não souber como fazer algo ou se não tiver certeza de que é possível, peça orientação ao Copilot.

### Encontrar o backlog criado pelo modelo

Quase todo projeto tem um backlog, e a Tailspin Toys não é exceção. Vamos explorar o backlog criado quando você usou o modelo.

1. Em **Sessions**, na barra lateral, selecione a pasta do repositório Tailspin Toys, e não uma sessão individual. Depois, selecione **Issues** na navegação superior do repositório.
2. Encontre estas issues pelo título, em vez de presumir seus números:

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Selecione uma issue para ler os detalhes. Cada issue também pode iniciar uma sessão de agente. Você começará pela issue de filtragem depois de fazer uma primeira alteração rápida.

> [!NOTE]
> As listas de itens em **Issues** e **Pull requests** são filtradas automaticamente para mostrar apenas os itens dos repositórios adicionados ao aplicativo Copilot. Para ver itens de outros repositórios, adicione-os ao aplicativo.

## Experimentar um chat rápido

Uma boa forma de conhecer o aplicativo é usá-lo para aprender sobre o próprio aplicativo. Um **chat rápido** é ideal para isso. Você pode fazer uma pergunta ou trocar ideias sem criar uma branch nem um worktree; é uma conversa curta que não exige uma sessão.

1. Na barra lateral, selecione **+** ao lado de **Chats** para abrir um novo chat. Se **Chats** ainda não estiver visível, selecione **+** ao lado de **Sessions** para iniciar seu primeiro chat; depois, **Chats** aparecerá.
2. Pergunte ao aplicativo como as sessões dele funcionam:

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. Leia a resposta na visualização da conversa. Cada sessão é executada em seu próprio worktree Git isolado, o que permite executar vários agentes em paralelo sem conflito entre as alterações. Você pode continuar a conversa ou iniciar um novo chat quando quiser.

## Resumo e próximos passos

Parabéns! Você instalou o aplicativo GitHub Copilot, conectou seu projeto e explorou o espaço de trabalho. Você aprendeu a:

- instalar o aplicativo e entrar na conta do GitHub.
- adicionar um projeto a partir do repositório do GitHub.
- conhecer o espaço de trabalho e encontrar o backlog em **Issues**.
- usar um chat rápido para fazer uma pergunta breve.

Em seguida, você [iniciará sua primeira sessão de agente][next-lesson] e exibirá uma classificação por estrelas nos cards de jogos.

## Recursos

- [Sobre o aplicativo GitHub Copilot][about-copilot-app]
- [Introdução ao aplicativo GitHub Copilot][getting-started]
- [Trabalhar com sessões de agente no aplicativo GitHub Copilot][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
[ghes-sign-in]: https://docs.github.com/enterprise-server@3.22/copilot/copilot-on-ghes/sign-in-on-copilot-app
