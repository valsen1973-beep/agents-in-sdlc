---
title: "レッスン 12 - GitHub Pages でサイトをデプロイする"
description: "GitHub Copilot app で Pages ワークフローを設定し、プルリクエストをレビューして、公開された Space Quiz を確認します。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

GitHub Pages を使って Space Quiz を公開しましょう。Copilot はワークフローの準備とデプロイを支援しますが、変更をレビューし、サイトが公開されたことを確認するのはあなたの役割です。

このレッスンでは、次のことを行います。

- Copilot に GitHub Pages のデプロイ設定を依頼します。
- マージする前にワークフローとプルリクエストをレビューします。
- デプロイの状況を追跡し、公開されたサイトを確認します。

## シナリオ

Space Quiz はすでに GitHub リポジトリにありますが、手軽に試す方法がありません。単一ファイルのサイトを GitHub Pages で公開すれば、サーバーや実行時依存関係を追加せずに公開 URL から利用できます。

## Copilot にデプロイの準備を依頼する

> [!WARNING]
> プルリクエストを作成すると、コードがコミットおよびプッシュされることがあります。プロンプトを送る前に、承認設定と送信先のリポジトリを確認してください。**Approve all** を選択している場合、個別の確認が表示されないことがあります。

`space-quiz` の Copilot app セッションで、次のプロンプトを送信します。

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## ワークフローとプルリクエストをレビューする

1. リポジトリに README がまだない場合に限り、README が追加されていることを確認します。
2. ワークフローのビルドとデプロイの手順、トリガー、権限を含め、プルリクエストの変更をレビューします。
3. ワークフローが、マージされていないプルリクエストではなく、既定のブランチからデプロイすることを確認します。
4. 必要な修正を依頼し、更新された差分をレビューします。マージを承認する前に、必要なプルリクエストのチェックがすべて成功するまで待ちます。

## マージとデプロイを承認する

> [!WARNING]
> 次のプロンプトを送ると、エージェントによるレビュー済みプルリクエストのマージ、リポジトリの Pages 設定の変更、サイトの公開を承認します。レビューを完了し、リポジトリとプルリクエストを確認してから送信してください。承認設定によっては、これらの操作に対して別の確認が表示されないことがあります。

`<PR_NUMBER>` をレビューしたプルリクエストの番号に置き換えてから、別のプロンプトとして送信します。

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![Space Quiz のプルリクエストのマージ、Build website、Upload artifact、Deploy to Pages の各ステップを含む GitHub Actions の Deploy website 実行の成功、yourname.github.io/space-quiz/ での公開サイトを示す3段階の図。](../../../_images/first-steps-app-pages-deploy.svg)

## デプロイを確認する

1. GitHub Actions のデプロイ実行が成功するまで確認します。
2. 報告された URL を開き、Space Quiz が表示されることを確認します。

エージェントが Pages の有効化やプルリクエストのマージを実行できない場合は、案内された手順に従ってください。デプロイが成功し、公開サイトが読み込まれるまで、完了と見なさないでください。

## まとめと次のステップ

Space Quiz が公開され、エージェントの報告だけに頼らずデプロイを確認できました。[レッスン 13: 振り返りと次のステップ][next-lesson]に進みます。

[next-lesson]: ../13-review/
