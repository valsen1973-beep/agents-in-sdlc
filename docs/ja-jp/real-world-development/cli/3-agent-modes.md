---
title: "レッスン 3 - エージェントモード: Plan と Autopilot"
description: "Plan で実装方法に合意し、Autopilot で Issue からフィルター機能を構築して、Interactive モードで結果を確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

最初に、小さな機能をプロジェクトに追加しました。より大きな変更には、さらにしっかりしたプロセスが必要です。GitHub Copilot CLI は組織の既存のワークフローに沿って動作し、適切なものを適切な方法で構築できるよう支援します。このレッスンから、典型的なエージェント主導の開発プロセスに沿って作業します。Issue を使って機能を作成し、コードの妥当性と機能の動作を確認して、最終的にプロジェクトへマージします。

> [!NOTE]
> 機能開発を続ける間、同じ会話とブランチを使用します。通常はファイル種別ごとにブランチや PR を分けますが、ここでは中心的な概念に集中するため手順を簡略化します。

このレッスンでは、次のことを行います。

- GitHub Issue から Copilot の会話を開始します。
- Plan モードで要件を決めます。
- Autopilot モードで機能を実装します。
- コードをレビューします。
- 転送ブラウザーで機能を手動検証します。

この後、リポジトリの指示を更新し、既存の `quality-checks` スキルをカスタマイズし、MCP による検証を追加して QA エージェントを作成し、機能 PR を開きます。

## シナリオ

Tailspin Toys のカタログが増え、利用者はカテゴリやパブリッシャーでゲームを絞り込む必要があります。バックログの Issue には機能が記載されていますが、カテゴリを組み合わせる方法など、コーディング前に合意が必要な詳細があります。Plan モードで決定し、その後、範囲を定めた実装を Autopilot に任せます。

## 背景

AI コーディングエージェントを開発ワークフローに加えても、基本は変わりません。一般的な開発フローは次のとおりです。

1. 実装内容を記載した Issue から始めます。
2. 構築する内容を計画します。
3. コードを作成してレビューします。
4. テストを実行してコードを検証します。
5. 新機能を手動で検証します。
6. プルリクエスト (PR) を作成します。
7. コードレビューと継続的インテグレーションが成功したら、コードをマージします。

> [!NOTE]
> 詳細な手順はチームや組織によって異なりますが、ほとんどの場合は上記の流れを基本にしています。

この標準的な進め方に従うことで、AI が生成したコードが要件を満たし、手書きのコードと同じレビューと検証を受けるようにできます。

## 会話モード

**会話モード**は、エージェントにどの程度の自律性を与えるかを決めます。<kbd>Shift</kbd>+<kbd>Tab</kbd> を押してモードを切り替えます。

- **Interactive**: エージェントと一緒に作業します。エージェントは変更を提案し、次に進む前に入力を待ちます。
- **Plan**: エージェントが最初に計画を作成します。プロジェクトファイルの編集はできません。
- **Autopilot**: エージェントが自律的にコードを書き、テストを実行し、タスクが完了するまで反復します。

まず Plan モードで計画を確認し、その後 Autopilot で実装します。

## Issue から始める

フィルター機能に取り組む前に、Codespace とターミナルを準備します。

1. Codespace に戻ります。停止している場合は再起動します。
2. 星評価の PR がマージ済みであることを確認します。
3. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
4. `main` を更新し、フィルター機能のブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

6. <kbd>Tab</kbd> を2回押して **Issues** タブを開きます。
7. <kbd>A</kbd> を押してすべての Issue を表示します。
8. 矢印キーで **Allow users to filter games by category and publisher** というタイトルの Issue を選択します。
9. <kbd>C</kbd> を押して Issue をプロンプトに追加し、**Session** タブに戻ります。

プロンプトの先頭に `#7` (または同様の番号) が表示されます。`#` を使うと、GitHub 上の Issue やプルリクエスト (PR) をコンテキストに追加できます。

## フィルター機能を計画する

計画を立てると、機能の実装やタスクの実行方法を決めてから Copilot に任せられます。複雑な作業では、事前に計画することをお勧めします。Plan モードに切り替え、Copilot に計画を作成してもらいましょう。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Plan モードに切り替え、プロンプトの下に **Plan** と表示されていることを確認します。
2. 前の手順で追加した Issue の後ろに、次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot はプロジェクトを調査して、最適な方法を決めます。

3. フィルター機能の動作について質問された場合は、希望に沿って回答します。唯一の正解はありません。
4. 計画が完成したら、<kbd>Control</kbd>+<kbd>E</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) を押して展開します。
5. 計画を読んで確認します。
6. 決定した内容と合わない部分があれば、Copilot に修正を依頼します。

## Autopilot を承認する

計画を確認したら、Autopilot で実装します。Autopilot は、タスクが完了したと判断するまで Copilot が問題に取り組むことを可能にします。

1. **Accept plan and build on autopilot (recommended)** またはインストール済みのバージョンにある同様の選択肢を選択します。
2. プロンプトの下に **Autopilot** と表示されていることを確認します。
3. Copilot が計画に沿ってコードを生成し、テストを実行する様子を確認します。

> [!NOTE]
> 承認すると実装がすぐに始まる場合があります。先に計画を確認してください。依存関係が不足している場合やポートが競合している場合は、チェック完了と見なす前にセットアップを修正します。

## 実装をレビューして検証する

ほかのコードと同様に、生成されたコードもマージ前にレビューします。コードを確認し、サイトを起動して動作を確認しましょう。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードに切り替え、モード表示が **Plan** や **Autopilot** ではないことを確認します。
2. `/diff` を入力し、フィルター機能の実装とテストを確認します。
3. 結果を Issue と計画時の決定に照らし合わせます。
4. レビュー後、<kbd>Esc</kbd> を押して差分画面を閉じます。
5. プロジェクトのチェック結果を確認し、失敗があれば Copilot に修正を依頼します。

## 新機能を試す

コードに問題がないように見えても、実行できるとは限りません。前回と同じようにアプリを起動し、Codespaces の転送ポートからサイトを開きます。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能になったら **Open in Browser** を選択します。
3. カテゴリ、パブリッシャー、および計画で合意した組み合わせで絞り込みます。
4. リセットと結果が空の場合の動作が、Issue と決定内容に沿っていることを確認します。
5. Codespace に戻り、起動した開発サーバーを停止するよう Copilot に依頼します。

## まとめと次のステップ

複数の会話モードを使って機能を構築し、レビューしました。Issue から会話を開始し、Plan モードで要件を決め、Autopilot モードで実装し、コードをレビューして、転送ブラウザーで手動検証しました。

次は、[カスタム指示を使ってコード生成を文書化された開発方針に沿わせます][next-lesson]。

## 参考資料

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI コマンドリファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
