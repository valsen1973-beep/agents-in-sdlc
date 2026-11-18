---
title: "Exercício 5: Iterar no trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

## Revisar o trabalho

Durante este laboratório, você trabalhou com o GitHub Copilot em várias tarefas para melhorar a experiência do usuário e adicionar funcionalidades. Você pediu ao Copilot que documentasse o código, criasse um recurso de jogos relacionados para a equipe de design avaliar e implementasse recursos de acessibilidade com seletores para os modos de alto contraste e claro. Vamos explorar as alterações e, se necessário, enviar comentários ao Copilot para melhorar o resultado.

### Cenário

Como já destacamos várias vezes, os fundamentos de design de software e DevOps não mudam com a chegada da IA generativa. Sempre devemos revisar o código gerado e seguir nosso processo normal de DevOps. Com isso em mente, vamos revisar as propostas do GitHub Copilot para a documentação, o recurso de jogos relacionados e os recursos de acessibilidade antes de habilitar a revisão pelo restante da equipe.

## Segurança e agente de nuvem do GitHub Copilot

Como o agente de nuvem executa tarefas de forma assíncrona e sem supervisão, há restrições de segurança para manter o ambiente protegido. Entre elas:

- O Copilot tem acesso de leitura ao repositório e acesso de escrita **somente** à branch que usará para o código.
- O agente de nuvem é executado no GitHub Actions, que cria um ambiente separado e temporário para o trabalho.
- Um ser humano precisa aprovar todos os workflows do GitHub Actions antes da execução.
- [O acesso a recursos externos é limitado por padrão](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluindo o acesso a servidores MCP.

## Revisar a documentação gerada

Vamos começar pelo primeiro pull request (PR) criado pelo agente de nuvem do GitHub Copilot: adicionar documentação ao código. Você fará essa revisão usando a interface padrão de PRs do GitHub.com.

> [!NOTE]
> Ao abrir o PR, você poderá ver um aviso de que o GitHub Copilot está bloqueado por um firewall. Isso é **esperado**, pois o acesso do Copilot a recursos externos, incluindo servidores MCP externos, é limitado por padrão. Se quiser, você pode [personalizar ou desabilitar o firewall do agente de nuvem][agent-firewall].

1. Volte ao seu repositório no github.com.
2. Selecione **Pull Requests** para abrir a lista de pull requests.
3. Abra o pull request com um título semelhante a **Add missing documentation** ou outro título mais completo.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando na tarefa, o pull request terá a marca **[WIP]**. Aguarde até que ele termine. Isso pode levar alguns minutos; aproveite para fazer uma pausa ou refletir sobre o que aprendeu.

4. Quando o pull request estiver pronto, selecione a guia **Files changed** e revise as alterações.

    ![Guia Files changed](../../../_images/shared-pr-files-changed.png)

5. Explore o código atualizado, que inclui os comentários TSDoc recém-criados e outras documentações. As alterações exatas variam.

   Ao examinar as alterações, procure comentários TSDoc, convenções de TypeScript e cabeçalhos de comentário. Eles vêm dos arquivos de instruções personalizadas que você revisou no início do Exercício 2.

6. Depois de revisar as atualizações e confirmar que estão corretas, volte à guia **Conversation** e role a página para baixo.
7. Você deverá ver um indicador de que alguns workflows estão aguardando aprovação.
8. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar workflows](../../../_images/shared-approve-workflows.png)

9. Os workflows deverão ser enfileirados na seção de verificações do pull request. Se tudo correr bem, as verificações do projeto para o aplicativo Astro único serão aprovadas. Isso pode levar alguns minutos.

## Solicitar alterações ao GitHub Copilot

Trabalhar com o Copilot em um pull request não é uma via de mão única. Você também pode marcar o Copilot em comentários do pull request — assim como faria com outra pessoa da equipe — ou em comentários no código. O Copilot verá esses comentários e iniciará outra sessão para resolvê-los. Como os resultados são não determinísticos, não há um texto prescritivo para solicitar alterações. Algumas sugestões:

- Adicionar cabeçalhos de comentário no início de cada arquivo de código, com uma breve descrição do conteúdo.
- Adicionar comentários TSDoc aos arquivos TypeScript e Astro.
- Criar um README que descreva a estrutura do aplicativo Astro.

1. Adicione um comentário solicitando uma alteração à documentação gerada e marque **@copilot** como faria com qualquer pessoa. Use uma das sugestões acima ou peça outra melhoria de documentação que gostaria de ver na base de código.
2. Selecione **View Session** para acompanhar o trabalho do Copilot. Observe que ele inicia uma nova sessão para fazer as atualizações.
3. Selecione **Back to pull request** para voltar ao pull request.

    ![Voltar ao pull request](../../../_images/ex7-back-to-pr.png)

4. Quando o Copilot terminar as alterações, deverá aparecer um novo commit no pull request.
5. Selecione a guia **Files changed** para revisar as alterações.

Continue iterando até ficar satisfeito. Depois, você pode marcar o PR como pronto para revisão e mesclá-lo à branch principal.

![Marcar o PR como pronto para revisão](../../../_images/ex7-ready-for-review.png)

## Revisar o recurso de jogos relacionados

Agora, vamos voltar ao PR que o Copilot criou para resolver a issue de exibir jogos relacionados na página de detalhes de cada jogo.

1. Volte ao seu repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione o PR com um título semelhante a **Show related games on the game details page** ou outro título mais completo.
4. Selecione a guia **Files changed** para revisar o código gerado.
5. Depois de revisar as atualizações e confirmar que estão corretas, volte à guia **Conversation** e role a página para baixo.
6. Você deverá ver um indicador de que alguns workflows estão aguardando aprovação.
7. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar workflows](../../../_images/shared-approve-workflows.png)

8. Os workflows deverão ser enfileirados na seção de verificações do pull request. Se tudo correr bem, as verificações do projeto para o aplicativo Astro único serão aprovadas. Isso pode levar alguns minutos.
9. **Opcional:** você também pode mudar para essa branch no Codespace para testar manualmente o recurso de jogos relacionados. Acesse o Codespace, abra o terminal e execute estes comandos, substituindo `<branch-name>` pelo nome da branch criada pelo Copilot, como **copilot/fix-8**:

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

O Copilot criou o recurso de jogos relacionados. Como antes, você pode iterar com o agente de nuvem e pedir atualizações. Por exemplo, talvez queira alterar a quantidade de jogos relacionados exibidos ou adicionar cabeçalhos de comentário e comentários TSDoc. Lembre-se: essa tarefa foi atribuída **antes** da atualização das instruções personalizadas. Para solicitar as alterações, adicione um comentário na guia **Conversation**; o Copilot iniciará uma nova sessão.

## Revisar os recursos de acessibilidade

Por fim, vamos revisar os recursos de acessibilidade implementados pelo agente personalizado de acessibilidade. Este PR deve incluir o modo de alto contraste atribuído no Exercício 3 e o modo claro solicitado no painel de controle no Exercício 4.

1. Volte ao seu repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione o PR com um título semelhante a **Add high contrast mode to website** ou outro título mais completo.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando na tarefa, o pull request terá a marca **[WIP]**. Aguarde até que ele termine. Isso pode levar alguns minutos.

4. Selecione a guia **Files changed** para revisar o código gerado.
5. Revise a implementação, prestando atenção especial a:
   - componentes de interface para alternar entre os modos.
   - uso do armazenamento local para manter as preferências.
   - alterações de CSS ou estilo dos modos de alto contraste e claro.
   - atributos de acessibilidade, como rótulos ARIA e navegação pelo teclado.
   - código JavaScript/TypeScript que gerencia a troca de modos.

6. Depois de revisar as atualizações e confirmar que estão corretas, volte à guia **Conversation** e role a página para baixo.
7. Você deverá ver um indicador de que alguns workflows estão aguardando aprovação.
8. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar workflows](../../../_images/shared-approve-workflows.png)

9. Os workflows deverão ser enfileirados na seção de verificações do pull request. Se tudo correr bem, as verificações do projeto para o aplicativo Astro único serão aprovadas. Isso pode levar alguns minutos.
10. **Opcional:** você pode mudar para essa branch no Codespace para testar manualmente os recursos de acessibilidade. Acesse o Codespace, abra o terminal e execute estes comandos, substituindo `<branch-name>` pelo nome da branch criada pelo Copilot:

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Em seguida, inicie o aplicativo e teste os seletores dos modos de alto contraste e claro no navegador. Confirme se funcionam como esperado e se as preferências permanecem após recarregar a página.

Observe como o agente personalizado de acessibilidade orientou o Copilot para implementar os recursos seguindo boas práticas de acessibilidade. Se encontrar problemas ou melhorias possíveis, marque **@copilot** em um comentário para solicitar atualizações, como fez com os PRs anteriores.

## Exercício opcional — continuar delegando

O agente de nuvem é mais útil quando você pode delegar itens reais do backlog e cuidar de outras tarefas. Para criar esse hábito, registre mais algumas issues no repositório e atribua-as ao Copilot. Algumas ideias:

- Criar um formulário para pessoas apoiadoras na página de detalhes do jogo.
- Implementar paginação na página de listagem de jogos.
- Adicionar validação de entrada e tratamento de erros aos helpers de acesso a dados.

## Resumo

Você concluiu o percurso do agente de nuvem. Ao longo destas lições, você:

- **Inspecionou os arquivos de instruções personalizadas deste repositório** para observar como influenciam o trabalho do agente de nuvem.
- **Atribuiu issues ao agente de nuvem do Copilot** e acompanhou a configuração do ambiente, o planejamento e a execução assíncrona.
- **Criou e usou um agente personalizado** para acessibilidade, adicionando seletores para os modos de alto contraste e claro.
- **Usou a página de agentes do Copilot como painel de controle** para acompanhar e orientar a sessão de acessibilidade durante a execução.
- **Revisou e ajustou os pull requests do agente de nuvem**, marcando `@copilot` para solicitar alterações e aprovando workflows.

## Revisão e próximos passos

Você concluiu o percurso do agente de nuvem. Para continuar explorando, os outros percursos complementam o que praticou:

- 🖥️ **[Percurso do VS Code](../../vscode/)** — explore o modo de agente do Copilot Chat e a integração com MCP diretamente no IDE.
- 💻 **[Percurso da CLI](../../cli/)** — entregue duas alterações revisadas pelo terminal com os modos Plan e Autopilot, skills de agente, um agente personalizado de QA, Playwright MCP, Agent Merge e uma ponte opcional `/delegate` para voltar ao agente de nuvem.

No seu próprio repositório, experimente estas ideias:

- Atribua ao agente de nuvem uma issue de refatoração ou de cobertura de testes.
- Crie um agente personalizado para outro domínio.
- Configure `copilot-setup-steps.yml` para outra stack.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre os agentes do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o workflow de configuração do agente de nuvem][cloud-agent-best-practices]
- [Configurar o firewall do agente de nuvem do Copilot][agent-firewall]

---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
