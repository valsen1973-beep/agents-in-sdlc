---
title: "Exercício 0: Pré-requisitos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de começar os exercícios do VS Code, prepare o ambiente. Você criará sua própria cópia do repositório Tailspin Toys, iniciará um [Codespace][codespaces] e confirmará que o GitHub Copilot Chat está funcionando no editor.

## Configurar o repositório do laboratório

Para criar uma cópia do repositório onde você desenvolverá, crie uma instância a partir do [modelo][template-repository]. A nova instância conterá todos os arquivos necessários para o laboratório.

1. Em uma nova janela do navegador, acesse o [modelo da Tailspin Toys][tailspin-template].
2. Crie sua cópia do repositório selecionando **Use this template** na página do repositório do laboratório. Em seguida, selecione **Create a new repository**.

    ![Botão Use this template](../../../_images/ex0-use-template.png)

3. Se você estiver fazendo o workshop como parte de um evento conduzido pelo GitHub ou pela Microsoft, siga as instruções dos mentores. Caso contrário, crie o novo repositório em uma organização na qual tenha acesso ao GitHub Copilot.

    ![Campos das configurações do repositório de modelo](../../../_images/ex0-repository-settings.png)

4. Anote o caminho do repositório criado (**organization-or-user-name/repository-name**), pois você o usará mais adiante no laboratório.

> [!NOTE]
> **Seu backlog está pronto**
>
> Ao criar o repositório a partir do modelo, um backlog de issues do GitHub é criado automaticamente. Você trabalhará com essas issues durante o workshop — não precisa criar nenhuma.

## Criar um Codespace

Em seguida, você usará um Codespace para concluir os exercícios.

[GitHub Codespaces][codespaces] é um ambiente de desenvolvimento na nuvem que permite escrever, executar e depurar código diretamente no navegador. Ele oferece um IDE completo com suporte a várias linguagens, extensões e ferramentas.

1. Acesse o repositório que você acabou de criar.
2. Selecione o botão verde **Code**.

    ![Botão Code selecionado](../../../_images/ex0-code-button.png)

3. Selecione a guia **Codespaces** e o botão **+** para criar um novo Codespace.

    ![Criação de um novo Codespace](../../../_images/ex0-create-codespace.png)

A criação do Codespace levará alguns minutos, embora ainda seja muito mais rápida do que instalar todos os serviços manualmente. Enquanto isso, você pode explorar outros recursos do GitHub Copilot.

> [!CAUTION]
> Você voltará ao Codespace em um exercício futuro. Por enquanto, mantenha-o aberto em uma guia do navegador.

> [!NOTE]
> Este workshop foi criado para ser executado em um Codespace ou em um [contêiner de desenvolvimento][dev-containers] local. Ambos garantem que o ambiente tenha os pré-requisitos necessários. Se preferir trabalhar localmente, abra o repositório clonado no VS Code e selecione **Reopen in Container** quando solicitado — o VS Code criará o mesmo contêiner de desenvolvimento usado pelo Codespace.

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## Usar o GitHub Copilot Chat e o modo de agente

Para acessar o modo de agente do GitHub Copilot Chat, instale a extensão GitHub Copilot Chat no IDE. Ela já deve estar disponível se você estiver usando um GitHub Codespace.

> [!TIP]
> Se a extensão GitHub Copilot Chat não estiver instalada, você pode [instalá-la pelo Visual Studio Code Marketplace][copilot-chat-extension]. Ou abra a visualização Extensions no Visual Studio Code, pesquise **GitHub Copilot Chat** e selecione **Install**.

Depois da instalação, talvez você precise autenticar sua conta do GitHub para habilitar a extensão.

1. Volte ao Codespace.
2. Se o Copilot Chat não aparecer à direita do editor, selecione o ícone **Copilot Chat** na parte superior do Codespace.
3. Digite uma mensagem, como "Hello world", na janela do Copilot Chat e pressione <kbd>Enter</kbd>. Isso deverá ativar o Copilot Chat.
4. Se você não estiver autenticado, será solicitado que entre na sua conta do GitHub. Siga as instruções para autenticar.

    ![Exemplo de solicitação de autenticação do Copilot Chat](../../../_images/ex1-copilot-authentication.png)

5. Depois da autenticação, a janela do Copilot Chat deverá aparecer.

## Resumo

Parabéns, você criou uma cópia do repositório do laboratório e começou a configurar o Codespace que usará para desenvolver.

## Próxima etapa

Vamos começar a usar o Copilot. Continue para [Exercício 1: Instruções personalizadas][next-lesson], onde você ensinará ao Copilot as convenções do projeto.

## Recursos

- [Visão geral do GitHub Codespaces][codespaces]
- [Criar um repositório a partir de um modelo][template-repository]
- [Introdução ao Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
