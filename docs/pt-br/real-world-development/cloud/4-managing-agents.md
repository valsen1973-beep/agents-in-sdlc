---
title: "Exercício 4 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Nos últimos exercícios, você pediu ao agente de nuvem do Copilot que executasse três tarefas distintas para melhorar a experiência do usuário e adicionar funcionalidades. Embora o agente de nuvem tenha sido desenvolvido para trabalhar de forma assíncrona e autônoma, ainda é importante acompanhar essas tarefas.

Há várias ferramentas para gerenciar as tarefas atribuídas ao agente de nuvem, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse painel de controle, você vê todas as tarefas do agente com pull requests (PRs) abertos. É possível explorar as operações realizadas e até orientar uma sessão em andamento.

Neste exercício, você vai:

- explorar a página de agentes para acompanhar as tarefas do agente de nuvem.
- orientar uma sessão em andamento para solicitar funcionalidades adicionais.

## Cenário

Depois de atribuir ao agente a tarefa de criar um modo de alto contraste, a equipe percebeu que seria um bom momento para adicionar também um modo claro. Como o agente já estava atualizando o estilo do site e adicionando um seletor de modo, pareceu lógico incluir esse recurso. Você orientará o agente para garantir que ele adicione o modo claro junto com o modo de alto contraste.

## Revisar as tarefas do agente de nuvem do Copilot

Vamos conferir o estado atual de todas as tarefas atribuídas ao agente de nuvem do Copilot.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Observe a lista de tarefas no painel principal e no painel esquerdo. Você deverá ver as tarefas atribuídas ao Copilot, incluindo:
   - atualizar a documentação da base de código.
   - gerar APIs para modificar jogos.
   - adicionar um modo de alto contraste ao site.
3. Selecione uma tarefa em andamento e revise as operações executadas pelo Copilot. Elas podem incluir:
   - obter o código do repositório.
   - criar o ambiente de trabalho do Copilot.
   - configurar servidores MCP.
   - executar várias etapas para concluir a tarefa.

> [!NOTE]
> As etapas exatas exibidas variam de acordo com o estado do trabalho do Copilot e a abordagem escolhida.

4. Observe também o painel de pull request no lado direito. Ele permite acompanhar o PR e os arquivos alterados.

## Orientar o agente de nuvem

Agora que você viu as tarefas em andamento, vamos pedir ao Copilot que inclua o modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão relacionada à adição do modo de alto contraste. O título exato varia de acordo com o nome usado pelo Copilot e o estado atual do trabalho.

    ![Sessão de acessibilidade no painel de controle](../../../_images/ex6-accessibility-session.png)

2. Acompanhe a sessão por alguns minutos, até que ela indique que a configuração terminou e o trabalho começou. Isso ficará evidente quando surgirem mensagens semelhantes aos exemplos.
3. Na caixa de diálogo **Steer active session while Copilot is working**, adicione o prompt:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Tarefa do agente de nuvem na página de agentes, com a caixa de diálogo de orientação da sessão ativa destacada](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe que o Copilot reconhece a solicitação e a incorpora ao trabalho.

## Deixar o Copilot trabalhar

Como antes, o Copilot começará a trabalhar na tarefa atualizada. Ele incorporará a nova solicitação quando terminar a etapa em que estava trabalhando no momento em que você enviou a mensagem.

Isso levará alguns minutos, então aproveite para fazer uma pausa e refletir sobre o que aprendeu até aqui.

## Resumo e próximos passos

Este exercício apresentou a página de agentes do Copilot, o ponto central para acompanhar e orientar tarefas do agente de nuvem do GitHub Copilot. Nesse painel de controle, você acompanha todas as tarefas ativas e concluídas, revisa o trabalho em andamento e redireciona tarefas para ajustar o escopo ou fornecer orientações adicionais.

Você explorou estes conceitos:

- explorar o painel de controle e a página de agentes para acompanhar tarefas do agente de nuvem.
- redirecionar uma sessão em andamento para solicitar funcionalidades adicionais.

Enquanto o Copilot conclui o trabalho de acessibilidade, vamos [iterar nos pull requests criados por ele][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar no trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
