---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Explore os modos de agente: use Plan para concordar com uma abordagem, Autopilot para criar a filtragem a partir de uma issue e Interactive para revisar e verificar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Começamos adicionando um pequeno recurso ao projeto. Alterações maiores exigem um processo mais robusto. Felizmente, o aplicativo GitHub Copilot foi desenvolvido para funcionar com o fluxo de trabalho existente da organização e ajudar a criar as coisas certas da maneira certa. Esta é a primeira de várias lições em que você seguirá um processo típico de desenvolvimento orientado por agentes: começará com uma issue para gerar um recurso, verificará se o código é válido e se o recurso se comporta como esperado e, por fim, fará a mesclagem no projeto.

> [!NOTE]
> Você continuará o fluxo de trabalho do recurso usando a mesma sessão. Normalmente, seriam usadas sessões ou PRs diferentes para os vários tipos de arquivo, mas faremos um atalho para focar nos conceitos principais.

Nesta lição, você vai:

- iniciar uma sessão de agente a partir de uma issue do GitHub.
- definir requisitos no modo **Plan**.
- implementar o recurso com o modo **Autopilot**.
- revisar o código.
- validar manualmente o recurso em um canvas de navegador.

Ao continuar o trabalho no recurso, você atualizará as instruções do repositório, personalizará a skill `quality-checks` existente, adicionará validação por MCP, criará um agente de QA e abrirá o PR do recurso.

## Cenário

O catálogo da Tailspin Toys está crescendo, e os visitantes precisam filtrar os jogos por categoria e editora. A issue do backlog descreve o recurso, mas detalhes como combinar categorias precisam ser acordados antes de escrever código. Você usará o modo Plan para decidir esses detalhes e, em seguida, autorizará uma implementação delimitada com o Autopilot.

## Contexto

Adicionar agentes de programação de IA ao fluxo de desenvolvimento não muda os fundamentos. Na verdade, eles se tornam ainda mais importantes. A maioria das pessoas desenvolvedoras segue um fluxo parecido com este:

1. Abrir uma issue registrada com os detalhes do trabalho necessário.
2. Criar um plano do que precisa ser implementado.
3. Criar e revisar o código.
4. Executar os testes para validar o código.
5. Validar manualmente a nova funcionalidade.
6. Criar um pull request (PR).
7. Depois que o código for revisado e o processo de integração contínua for concluído com sucesso, mesclar o código.

> [!NOTE]
> Os detalhes exatos variam de acordo com a equipe e a organização, mas a maioria segue uma variação do fluxo acima.

Seguir essa abordagem padrão ajuda a garantir que o código gerado por IA atenda aos requisitos e passe pelo mesmo processo de validação do código escrito manualmente.

## Modos de sessão

O **modo de sessão** controla o nível de autonomia do agente. Você pode defini-lo no menu suspenso abaixo do campo de prompt e alterá-lo quando quiser:

- **Interactive**: você e o agente trabalham em conjunto. O agente sugere alterações e aguarda sua resposta antes de continuar.
- **Plan**: o agente cria primeiro um plano. Você revisa e aprova o plano antes da execução.
- **Autopilot**: o agente trabalha de forma totalmente autônoma, escrevendo código, executando testes e iterando sem esperar sua resposta.

Comece no modo Plan, revise o plano e depois use o Autopilot para implementá-lo.

## Iniciar uma sessão a partir da issue

Confirme que o PR de classificação por estrelas foi mesclado e que sua `main` local está atualizada antes de continuar.

1. Em **Sessions**, na barra lateral, selecione a pasta do repositório Tailspin Toys e, na navegação superior do repositório, selecione **Issues**. Abra **Allow users to filter games by category and publisher**. Essa issue já foi criada pelo modelo; não é necessário criar outra.
2. Selecione **New session** e escolha uma **nova árvore de trabalho** baseada na `main` atualizada.

   ![Visualização da issue no aplicativo GitHub Copilot com uma seta apontando para o botão New session](../../../_images/app-new-session-from-issue.png)

3. Confirme que a issue foi anexada à sessão e selecione **Plan** no seletor de modo.

> [!NOTE]
> Se o Node.js ou o npm não forem encontrados, peça ao agente que execute `node --version` e `npm --version`. Se os comandos funcionarem no terminal, mas não na sessão, verifique o PATH do aplicativo ou a configuração do gerenciador de versões e feche e reabra o aplicativo completamente. Repita a operação e as verificações que falharam; não reinstale o npm apenas porque o agente não consegue encontrá-lo.

## Planejar o recurso de filtragem

O planejamento permite revisar a abordagem antes que o Copilot escreva código. Como você iniciou pela issue, o Copilot já tem a solicitação do recurso no contexto. Envie:

```plaintext
Build this feature.
```

Responda às perguntas do Copilot e compare o plano com os critérios de aceitação da issue. Confirme se ele inclui a filtragem por categoria e editora, controles acessíveis, alterações de acesso a dados e testes. Converse sobre qualquer comportamento pouco claro, como a forma de combinar várias categorias ou o que acontece quando nenhum jogo corresponde.

O plano deve incluir lint, testes unitários, testes E2E e verificação de tipos com as ferramentas existentes do projeto. Mantenha o escopo focado em implementar e testar a filtragem; você criará o PR depois de concluir o fluxo de qualidade. Peça as alterações necessárias ao plano antes de aprová-lo e guarde a URL da issue e quaisquer esclarecimentos acordados para a validação posterior.

## Aprovar explicitamente o Autopilot

Quando estiver satisfeito com o plano, selecione **Approve and implement this plan** ou a opção equivalente na sua versão. Confira o modo ativo; não presuma que a aprovação o altera automaticamente. Confirme que o indicador de modo mostra **Autopilot**.

O Copilot começará a implementar o recurso. Ele seguirá o plano, gerará código e executará testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente, portanto revise o plano primeiro. Se o Copilot informar que faltam dependências ou que há um conflito de portas, resolva o problema de configuração antes de considerar as verificações concluídas. Pare somente os servidores que você iniciou.

## Revisar e verificar a implementação

Depois que o código for gerado, ele precisa ser revisado antes da mesclagem, como qualquer outro código. Vamos revisar o código e executar o site para confirmar que tudo funciona.

1. Abra **Changes** e inspecione a implementação da filtragem e os testes.
2. Compare o resultado com a issue e os esclarecimentos aprovados, incluindo as combinações de categorias e editoras. Confirme que as alterações seguem as instruções existentes do repositório.
3. Examine os resultados de lint, testes unitários, testes E2E e verificação de tipos. Uma verificação ignorada não significa aprovação.
4. Resolva as falhas e execute novamente as verificações afetadas antes de aceitar a implementação. A configuração E2E do Playwright cria e disponibiliza uma prévia e pode reutilizar um servidor local. Confirme que o servidor usado nos testes pertence a este worktree, e não a uma lição anterior.

## Explorar a nova funcionalidade

O código parece correto, mas será que funciona? Vamos iniciar o aplicativo como fizemos antes e abrir o site em um canvas de navegador.

1. Use o prompt a seguir para pedir ao Copilot que inicie o aplicativo e abra a página no canvas de navegador:

   ```plaintext
   Start the app and open it in the browser canvas.
   ```

2. Em alguns instantes, o aplicativo será iniciado e uma janela do navegador aparecerá dentro do aplicativo Copilot.
3. Selecione uma categoria e confirme se os resultados correspondem a ela. Limpe o filtro, selecione uma editora e confirme os resultados.
4. Combine filtros de categoria e editora e compare os resultados com a issue e o plano aprovado. Se houver suporte a várias categorias, verifique o comportamento combinado acordado.
5. Teste uma combinação sem jogos correspondentes e confira o estado vazio. Limpe ou redefina os filtros e confirme que a lista completa volta a aparecer.
6. Quando terminar, peça ao Copilot que pare o servidor de desenvolvimento iniciado para esta sessão:

   ```plaintext
   Stop the dev server and close the browser canvas.
   ```

## Manter esta sessão para as próximas lições

Ainda não crie nem mescle o PR de filtragem. Mantenha esta sessão, este worktree e esta branch para as Lições 4 a 8. Em seguida, você aplicará instruções personalizadas ao código de filtragem e adicionará melhorias à skill e ao agente de QA antes de criar e mesclar o PR combinado na Lição 8. Depois de parar o servidor de desenvolvimento, você pode deixar a sessão ociosa e retomá-la na próxima lição.

## Resumo e próximos passos

Você usou diferentes modos de agente para criar e revisar um recurso. Nesta lição, você:

- iniciou uma sessão de agente a partir de uma issue do GitHub.
- definiu requisitos no modo **Plan**.
- implementou o recurso com o modo **Autopilot**.
- revisou o código.
- validou manualmente o recurso em um canvas de navegador.

Em seguida, vamos entender melhor como o código é gerado e garantir que siga as práticas documentadas [usando instruções personalizadas][next-lesson].

## Recursos

- [Trabalhar com sessões de agente no aplicativo GitHub Copilot][agent-sessions]

[next-lesson]: ../4-custom-instructions/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
