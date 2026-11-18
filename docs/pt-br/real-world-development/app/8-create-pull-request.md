---
title: "Lição 8 - Criar e mesclar o PR do recurso"
description: "Revise a filtragem, as instruções, a atualização da skill, o perfil de QA e os testes; depois crie um PR e use o Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

A implementação da filtragem, as atualizações das instruções, a atualização da skill, o perfil de garantia de qualidade (QA) e os testes estão salvos em uma única branch. Agora é hora de revisá-los em conjunto e abrir um pull request. Você mesmo mesclou o pull request (PR) de classificação por estrelas; desta vez, deixará que o **Agent Merge** gerencie o processo.

> [!NOTE]
> Normalmente, dividiríamos o recurso, as atualizações das instruções, a atualização da skill e o agente de QA em alguns PRs separados. Para simplificar o workshop, mantivemos todo o fluxo de filtragem e qualidade em uma sessão e branch, e incluiremos o trabalho neste PR.

Nesta lição, você vai:

- aprender o que é o Agent Merge e como ele automatiza o ciclo de vida da mesclagem.
- inspecionar o PR do recurso completo e as evidências de verificação.
- autorizar o Agent Merge somente depois da revisão e confirmar que o PR foi mesclado.

## Cenário

Durante o fluxo de filtragem, você usou o Copilot para planejar, implementar e verificar um recurso. Agora, a Tailspin Toys quer automatizar o trabalho restante do PR, mantendo a autorização de mesclagem sob o controle da pessoa desenvolvedora.

## Apresentação do Agent Merge

O **Agent Merge** automatiza o trabalho restante para concluir um pull request no aplicativo GitHub Copilot. Quando você o habilita, a sessão do aplicativo lê o pull request e resolve o que estiver bloqueando-o — corrigindo verificações de integração contínua (CI) com falha, respondendo a comentários de revisão e fazendo rebase quando necessário — e o mescla assim que o GitHub permitir. Ele funciona em segundo plano, continua após a reinicialização do aplicativo e é desativado quando o pull request é mesclado.

Até aqui, você selecionou **Merge pull request** manualmente. O Agent Merge pode assumir essa responsabilidade, mas a capacidade de editar código e mesclar ainda exige sua autorização explícita. Revise as ações permitidas e o trabalho antes de conceder permissão para mesclar.

## Usar o Agent Merge para gerenciar o PR

Com todo o código criado e revisado, vamos deixar que o Agent Merge gerencie o processo do PR.

1. Use o seletor de agentes para escolher **Default agent**.
2. Selecione a seta ao lado de **Create PR**.
3. Selecione **Agent Merge**. O botão mudará para **Agent Merge**.
4. Selecione o botão **Agent Merge** para iniciar o processo. Escolher a opção na lista, por si só, não inicia o processo.

O Agent Merge começará a trabalhar. Ele:

- criará o pull request com título e descrição.
- se a sessão tiver começado a partir de uma issue, fará referência à issue na descrição.
- fará rebase ou resolverá possíveis conflitos com a branch de destino.
- acompanhará a CI e confirmará que todas as verificações foram aprovadas.
- acompanhará os comentários no PR de outras pessoas desenvolvedoras ou da revisão de código do Copilot e fará alterações para resolver as observações.
- poderá mesclar automaticamente o PR depois que tudo for concluído com sucesso.

Vamos permitir que o Agent Merge também mescle o PR depois que todas as verificações forem aprovadas.

5. Revise o diff do PR e as evidências de verificação antes de conceder permissão para mesclar.
6. Selecione a seta ao lado de **Agent Merge**.
7. Confirme se há uma marca ao lado de **Merge pull request**.
8. Peça explicitamente ao agente que faça a mesclagem:

   ```plaintext
   Merge the PR once all required checks and approvals pass. Do not bypass repository protections.
   ```

9. Acompanhe o progresso e resolva os bloqueios relatados. Confirme que o estado do PR é **Merged** antes de continuar. Ter habilitado a permissão de mesclagem ou um agente em execução não confirma que a mesclagem foi concluída.

> [!IMPORTANT]
> O Agent Merge não ignora as proteções do repositório nem permissões ausentes. Resolva esses bloqueios antes de continuar.

## Resumo e próximos passos

Você automatizou várias partes do processo de desenvolvimento: geração de código, teste e validação e, agora, o processo do pull request. Você:

- aprendeu o que é o Agent Merge e como ele automatiza o ciclo de vida da mesclagem.
- inspecionou o PR do recurso completo e as evidências de verificação.
- autorizou o Agent Merge somente após a revisão e confirmou que o PR foi mesclado.

Em seguida, você [usará um canvas existente e criará um canvas de triagem][next-lesson] para explorar uma forma mais avançada de inspecionar, planejar e visualizar o trabalho com o agente.

## Recursos

- [Gerenciar issues e pull requests com o aplicativo GitHub Copilot][managing-issues-prs]
- [Sobre o aplicativo GitHub Copilot][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
