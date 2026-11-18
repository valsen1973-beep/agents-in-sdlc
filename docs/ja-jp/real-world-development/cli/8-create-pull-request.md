---
title: "レッスン 8 - 機能 PR の作成とマージ"
description: "フィルター機能、指示、スキルの更新、QA プロファイル、テストを確認して PR を作成し、Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

フィルター機能の実装、指示の更新、スキルの更新、品質保証 (QA) プロファイル、テストは、1つのブランチに保存されています。まとめてレビューし、プルリクエストを作成しましょう。星評価の PR は手動でマージしましたが、今回は **Agent Merge** にマージの流れを管理させます。

> [!NOTE]
> 通常は機能、指示の更新、スキル、QA エージェントを複数の PR に分けます。このワークショップでは、手順を簡潔にするためフィルター機能と品質に関する作業を1つの会話とブランチで進め、この PR にまとめました。

このレッスンでは、次のことを行います。

- Agent Merge と、マージのライフサイクルを自動化する方法を学びます。
- 機能全体の変更と検証結果を調べます。
- フィルター機能の PR を作成します。
- レビュー後に Agent Merge を有効にして、PR がマージされたことを確認します。

## シナリオ

フィルター機能の開発では、Copilot を使って計画、実装、検証を行いました。Tailspin Toys では、マージを承認する権限は開発者が保持したまま、残りの PR 作業を自動化したいと考えています。

## Agent Merge について

**Agent Merge** は、プルリクエストをマージ可能にするための残りの作業を自動化します。有効にすると、Copilot は CI チェックの失敗を修正し、レビューコメントに対応し、必要に応じてリベースするなど、PR を妨げている問題を解決します。その後、リポジトリで許可されていれば GitHub の自動マージを有効にします。

これまでは自分で **Merge pull request** を選択していました。Agent Merge に任せることもできますが、有効化する前に変更をレビューし、マージ準備ができていると判断してください。

## Agent Merge で PR を管理する

コードを作成したので、まとめてレビューし、PR を作成して、残りの処理を Agent Merge に任せます。

1. Codespace に戻ります。
2. `/agent` を入力してエージェントダイアログを開きます。
3. 一覧から **Default** を選択し、<kbd>Enter</kbd> を押します。
4. `/pr create` コマンドで新しい PR を作成します。
5. `/pr agentmerge` で Agent Merge を有効にします。
6. Copilot は PR の継続的インテグレーションを監視し、すべて成功したらマージします。
7. `PR #14 was squash-merged successfully.` のようなメッセージが表示されたことを確認します。

> [!IMPORTANT]
> Agent Merge は、必須の承認、ブランチ保護、マージキュー、リポジトリ設定、権限不足を回避しません。処理がブロックされた場合は理由を確認し、リポジトリで許可される場合はレビュー済みの PR を手動でマージしてください。

## まとめと次のステップ

コード生成、テストと検証、プルリクエストの処理など、開発プロセスの一部を自動化しました。Agent Merge を学び、機能全体と検証結果を確認し、フィルター機能の PR を作成して、レビュー後に Agent Merge を有効にしました。

次は、コンテキスト、モデル、共有、任意のクラウド委任に使える[便利な Copilot CLI slash command を確認します][next-lesson]。

## 参考資料

- [Copilot CLI でプルリクエストを管理する][manage-prs]
- [Copilot CLI コマンドリファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
