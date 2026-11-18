---
title: "レッスン 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前のレッスンでは、ユーザー体験の改善と機能追加を目的に、Copilot cloud agent に3つのタスクを依頼しました。cloud agent は非同期かつ自律的に作業しますが、進行中のタスクを監視することも大切です。

cloud agent に割り当てたタスクは、GitHub.com の[エージェントページ][agents-page]など、さまざまな方法で管理できます。この Mission control では、オープンなプルリクエスト (PR) があるエージェントタスクを一覧できます。実行内容を確認し、進行中のセッションに追加の指示を送ることもできます。

このレッスンでは、次のことを行います。

- エージェントページで cloud agent のタスクを監視します。
- 進行中のセッションに指示を送り、機能追加を依頼します。

## シナリオ

チームはハイコントラストモードの作成をエージェントに依頼した後、ライトモードも追加することにしました。サイトのスタイルと切り替え機能をすでに更新しているため、ライトモードも含めるのが自然です。エージェントの作業に指示を送り、ハイコントラストに加えてライトモードも追加してもらいます。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたタスクの現在の状況を確認します。

1. [Copilot agents ページ](https://github.com/copilot/agents)を開きます。
2. メインペインと左ペインの両方にあるタスク一覧を確認します。次のようなタスクが表示されます。
   - コードのドキュメントを更新する
   - ゲームを更新する API を生成する
   - Web サイトにハイコントラストモードを追加する
3. 実行中のタスクを1つ選択し、Copilot が実行した作業を確認します。たとえば、次の内容が含まれます。
   - リポジトリのチェックアウト
   - Copilot の作業環境の作成
   - MCP サーバーのセットアップ
   - タスク完了に向けた各種の処理

> [!NOTE]
> 表示される手順は、Copilot の進捗状況や作業方法によって異なります。

4. 右側に表示される PR ペインも確認します。ここから PR と変更ファイルを確認し、作業を監視できます。

## Cloud agent に指示を送る

実行中のタスクを確認できたので、ハイコントラストモードの作業中にライトモードも追加するよう Copilot に依頼します。

1. ハイコントラストモードを追加しているセッションを選択します。表示されるタイトルは Copilot が付けた名前や作業の進捗によって異なります。

    ![Mission control のアクセシビリティセッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが終わり、作業が始まったことを示すメッセージが表示されるまで数分待ちます。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![エージェントページで、Steer active session while Copilot is working ダイアログを強調表示したスクリーンショット](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot が依頼を認識し、作業に追加したことを確認します。

## Copilot の作業を待つ

Copilot は更新されたタスクに取り組みます。メッセージを送信した時点で実行していた手順が終わると、新しい依頼を作業に反映します。

完了まで数分かかります。その間に、これまでに学んだことを振り返りましょう。

## まとめと次のステップ

このレッスンでは、Copilot cloud agent のタスクを監視し、方向付ける中心的な場所である Copilot agents ページを確認しました。Mission control では、実行中と完了済みのタスクを追跡し、作業内容を確認して、進行中のセッションに追加の指示を送れます。

次の内容を確認しました。

- Mission control とエージェントページで cloud agent のタスクを監視する
- 進行中のセッションに指示を送り、機能追加を依頼する

Copilot がアクセシビリティ機能を実装している間に、次は [Copilot が作成したプルリクエストを反復して改善します][next-lesson]。

## 参考資料

- [Copilot agents ページ][agents-page]
- [カスタムエージェントについて][custom-agents]

---

| [← 前のレッスン: カスタムエージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復して改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
