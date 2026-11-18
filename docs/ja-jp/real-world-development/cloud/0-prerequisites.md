---
title: "レッスン 0: 前提条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Copilot cloud agent の演習を始める前に、必要なものを準備します。Tailspin Toys リポジトリの自分用コピーを作成し、[Codespace][codespaces] を起動します。Codespace では指示ファイルを編集し、cloud agent が作成した変更をレビューできます。

## ワークショップ用リポジトリのセットアップ

作業用のリポジトリを用意するには、[テンプレート][template-repository]から自分用のインスタンスを作成します。新しいリポジトリには演習に必要なファイルが含まれており、ワークショップ中に使用します。

1. 新しいブラウザーウィンドウで [Tailspin Toys テンプレート][tailspin-template]を開きます。
2. ワークショップ用リポジトリのページで **Use this template** を選択し、続けて **Create a new repository** を選択して、自分用のコピーを作成します。

    ![Use this template ボタン](../../../_images/ex0-use-template.png)

3. GitHub または Microsoft が主催するイベントでワークショップに参加している場合は、メンターの案内に従ってください。それ以外の場合は、GitHub Copilot を利用できる組織に新しいリポジトリを作成します。

    ![リポジトリテンプレートの設定を入力する画面](../../../_images/ex0-repository-settings.png)

4. 作成したリポジトリのパス (**organization-or-user-name/repository-name**) を控えてください。この後の演習で使用します。

## Codespace の作成

続いて、演習で使う Codespace を作成します。

[GitHub Codespaces][codespaces] は、ブラウザーからコードを作成、実行、デバッグできるクラウド開発環境です。複数のプログラミング言語、拡張機能、ツールに対応した IDE を利用できます。

1. 作成したリポジトリを開きます。
2. 緑色の **Code** ボタンを選択します。

    ![Code ボタンを選択する](../../../_images/ex0-code-button.png)

3. **Codespaces** タブを選び、**+** ボタンを選択して新しい Codespace を作成します。

    ![新しい Codespace を作成する](../../../_images/ex0-create-codespace.png)

Codespace の作成には数分かかりますが、必要なサービスを手動でインストールするよりも早く完了します。作成中に、次に紹介する GitHub Copilot の機能を確認してみましょう。

> [!CAUTION]
> 今後の演習でこの Codespace に戻ります。今はブラウザーのタブを閉じずに開いたままにしてください。

> [!NOTE]
> このワークショップは Codespace またはローカルの [dev container][dev-containers] で実行できます。どちらも、スムーズに作業できるよう必要な前提条件がインストールされた環境です。ローカルで実行する場合は、クローンしたリポジトリを VS Code で開き、プロンプトが表示されたら **Reopen in Container** を選択してください。Codespace と同じ dev container が構築されます。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## まとめ

ワークショップ用リポジトリを作成できました。Copilot cloud agent と一緒に作業するための Codespace も作成を開始しました。

## 次のステップ

次は、cloud agent が従うカスタム指示を追加します。[レッスン 1 - カスタム指示][next-lesson]に進んでください。

## 参考資料

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces の使用を開始する][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
