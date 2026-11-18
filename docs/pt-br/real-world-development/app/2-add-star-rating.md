---
title: "Lição 2 - Adicionar classificações por estrelas: uma vitória rápida"
description: "Inicie sua primeira sessão de agente no aplicativo GitHub Copilot, faça uma pequena alteração nos cards de jogos e mescle seu primeiro pull request."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Agora que você conheceu o espaço de trabalho e experimentou um chat rápido, é hora de iniciar uma **sessão de agente** e fazer sua primeira alteração no projeto. Ela será pequena: os dados dos jogos já incluem uma classificação por estrelas, mas os cards da página inicial ainda não a exibem. Você pedirá ao agente que mostre a classificação, revisará a alteração e a mesclará como seu primeiro pull request.

Nesta lição, você vai:

- iniciar uma sessão de agente e conhecer a estrutura de uma sessão.
- pedir ao agente que faça uma pequena alteração focada no projeto.
- revisar a alteração na visualização de diff do espaço de trabalho.
- executar o aplicativo localmente para confirmar a alteração no navegador.
- abrir e mesclar seu primeiro pull request.

## Cenário

Cada jogo da Tailspin Toys pode ter uma classificação por estrelas, que já aparece na página de detalhes do jogo. Os cards da página inicial, porém, mostram apenas o título, a categoria, a editora e a descrição. Como aquecimento, você pedirá ao agente que exiba a classificação existente em cada card — uma alteração pequena e independente, ideal para sua primeira sessão.

## Anatomia de uma sessão

Uma **sessão** é uma conversa com um agente executada em seu próprio espaço de trabalho isolado. Cada sessão tem um **worktree e uma branch Git dedicados**, o que permite executar várias sessões ao mesmo tempo — uma para adicionar uma funcionalidade e outra para corrigir um bug, por exemplo — sem conflito entre as alterações. As sessões aparecem na barra lateral, agrupadas por repositório. Selecione uma delas para alternar.

Em uma sessão, você verá três coisas: a **conversa** com o agente, a **atividade das ferramentas** enquanto ele explora e edita arquivos e a lista de **arquivos alterados** com seus diffs.

## Iniciar uma sessão e solicitar a alteração

Vamos iniciar uma nova sessão para explorar o projeto e implementar o recurso. Durante a [configuração do aplicativo][prior-lesson], você adicionou o projeto a partir do repositório do GitHub. Agora, criaremos uma sessão para esse repositório e solicitaremos a alteração.

1. Volte ao aplicativo GitHub Copilot ou abra-o.
2. Selecione **+** no início da barra lateral para iniciar uma sessão.
3. Selecione `tailspin-toys` como repositório.
4. Abaixo da caixa de prompt, escolha uma **nova árvore de trabalho** e o modo **Interactive**. Use o prompt a seguir para solicitar a alteração:

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

5. Pressione <kbd>Enter</kbd> para enviar o prompt ao Copilot.

O aplicativo Copilot começa criando um novo worktree, uma cópia isolada do projeto. Depois, explora o projeto, localiza os arquivos que precisam ser alterados e cria o código necessário. Você acaba de adicionar um recurso com o aplicativo Copilot.

## Revisar o diff

Todas as alterações geradas por IA devem ser revisadas antes da mesclagem, mesmo as pequenas. Vamos explorar as alterações aqui mesmo no aplicativo Copilot.

1. No canto superior direito do aplicativo, selecione **Toggle review panel**. No painel que abrir, selecione **Changes** para ver os arquivos alterados e seus diffs.

   ![Barra de ferramentas superior do aplicativo GitHub Copilot com uma seta apontando para o botão Toggle review panel à direita de Create PR](../../../_images/app-2-review-panel.png)

2. Você deverá ver código adicionado a `GameCard.astro`, o arquivo principal usado para exibir os detalhes dos jogos. Ele deverá ser semelhante ao trecho a seguir: um bloco pequeno que mostra a classificação, quando disponível, e usa "No rating yet" quando `starRating` é `null`.

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Como todas as ferramentas de IA generativa, o Copilot é probabilístico, e não determinístico. O código exato pode variar, mas deverá ser parecido com o exemplo.

## Verificar as alterações

Revise os resultados das verificações automatizadas do agente antes de abrir o navegador. Confirme que os testes cobrem uma classificação numérica em `starRating` e a alternativa `null`. Uma verificação ignorada ou um pré-requisito ausente não significa aprovação; revise qualquer solicitação de instalação antes de aprová-la.

Não devemos apenas ler o código e presumir que funciona. Vamos pedir ao Copilot que abra o site para examinarmos a interface atualizada. Ele iniciará o site e o abrirá em um canvas de navegador.

> [!TIP]
> Um canvas é um widget interativo disponível dentro do aplicativo Copilot. Você explorará canvases personalizados e criará um mais adiante; por enquanto, usaremos o canvas de navegador integrado.

1. Use o prompt a seguir para pedir ao Copilot que inicie o aplicativo e abra a página no canvas de navegador:

   ```plaintext
   Start the app and open it in the browser canvas.
   ```

2. Em alguns instantes, o aplicativo será iniciado e uma janela do navegador aparecerá dentro do aplicativo Copilot.
3. Confirme que os cards de jogos classificados exibem o valor de zero a cinco.
4. Quando terminar, peça ao Copilot que pare o servidor de desenvolvimento iniciado para esta sessão:

   ```plaintext
   Stop the dev server and close the browser canvas.
   ```

## Abrir e mesclar seu primeiro pull request

Você criou o recurso! Agora, abra um pull request (PR) para mesclar o novo código à base de código existente.

1. Selecione **Create PR** no canto superior direito.
2. Se solicitado, selecione **Sign in with your browser** e siga as instruções para autenticar.
3. Se o Copilot explicar que a política do repositório exige uma issue correspondente antes da criação do PR, confirme que ele deve seguir esse processo.
4. O Copilot criará o PR.
5. Selecione o indicador **PR** logo acima do chat para abrir o pull request no painel de revisão.
6. Quando estiver tudo pronto, selecione **Ready to merge**.
7. Na nova janela, selecione **Merge pull request** para mesclar seu pull request.

## Resumo e próximos passos

Parabéns! Você entregou sua primeira alteração usando o aplicativo GitHub Copilot. Em especial, você:

- iniciou uma sessão de agente e conheceu a estrutura de uma sessão.
- orientou o agente a fazer uma pequena alteração focada nos cards de jogos.
- revisou a alteração na visualização de diff do espaço de trabalho.
- executou o aplicativo localmente para confirmar a classificação por estrelas no navegador.
- abriu o PR 1, revisou as verificações e fez a mesclagem explicitamente.

Em seguida, você [começará pela issue de filtragem e usará os modos Plan e Autopilot][next-lesson] para criar um recurso maior.

## Recursos

- [Trabalhar com sessões de agente no aplicativo GitHub Copilot][agent-sessions]
- [Sobre o aplicativo GitHub Copilot][about-copilot-app]
- [Gerenciar issues e pull requests com o aplicativo GitHub Copilot][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#instalar-e-configurar-o-aplicativo-github-copilot
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
