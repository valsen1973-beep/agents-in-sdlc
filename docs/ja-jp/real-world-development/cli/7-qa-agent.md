---
title: "レッスン 7 - QA エージェントの作成と使用"
description: "Issue の要件、quality-checks スキル、Playwright MCP を組み合わせる QA カスタムエージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

`quality-checks` スキルで自動チェックを実行し、Playwright MCP でブラウザーからフィルター機能を確認しました。今度は明確な QA プロセスを持つカスタムエージェントに、これらの機能をまとめます。

このレッスンでは、次のことを行います。

- カスタムエージェントが指示、スキル、MCP ツールと連携する方法を確認します。
- 再利用可能な品質保証プロファイルを作成して調べます。
- QA エージェントを選び、フィルター機能の Issue に照らして報告を確認します。

## シナリオ

Tailspin Toys では、プルリクエスト (PR) を作成する前に、要件、コード品質、自動チェック、テストカバレッジ、ブラウザーでの動作を一貫して確認したいと考えています。カスタムエージェントで QA プロセスを調整し、再利用可能な報告を作成できます。

## カスタムエージェントとは

カスタムエージェントは、目的、指示、利用できるツールを記述した Markdown プロファイルで定義する、専門化された Copilot です。このワークショップでは、`.github/agents/qa.agent.md` に QA の役割を定義し、Copilot CLI で選択します。

これまでに使ったカスタマイズには、それぞれ異なる役割があります。リポジトリの指示はチームの標準を示します。`quality-checks` スキルは繰り返し実行できるチェックをまとめます。Playwright MCP はブラウザーツールを提供します。QA プロファイルは、これらを使って要件を評価し、結果を報告するよう Copilot に指示します。ほかの機能を置き換えるものではなく、新しい会話も必要ありません。

## QA プロファイルを作成する

機能の PR を開く前に、再利用できる QA プロファイルを Copilot に作成してもらいます。QA の確認項目と制約の両方を定義します。

1. Codespace に戻り、フィルター機能の会話が Interactive モードであることを確認します。
2. 既定のエージェントに、次のカスタムエージェントを作成するよう依頼します。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

エージェントを使う前に、プロファイルに意図した QA の手順と制約が記載されていることを確認します。これにより、検証だけを依頼したのに不完全または広範な変更を加えることを防げます。

1. `/diff` を入力し、`.github/agents/qa.agent.md` を開きます。
2. フロントマターを確認します。`description` は必須です。`name` は省略できますが、含めるとエージェントを識別しやすくなります。
3. プロファイルを読み、要件から確認を始めること、リポジトリの指示に従うこと、`quality-checks` スキルを実行すること、Playwright MCP を使うことを確認します。
4. 根拠を示して報告すること、実装コードを変更する前に確認を求めること、コミットやプルリクエストの作成をしないことを確認します。
5. 不足や過剰な指示がある場合は、既定のエージェントに修正を依頼してから次に進みます。

## Issue に対して QA を実行する

Copilot CLI は会話開始時にプロジェクトのエージェントを読み込みます。プロファイル作成後に同じフィルター機能の会話を再開し、QA を選ぶと、Issue と計画の内容を引き継げます。

1. 次のプロンプトでエージェントを有効にします。

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 作成したばかりのエージェントが一覧に表示されない場合がありますが、上記コマンドで有効にできます。

2. 次のプロンプトで機能の確認を依頼します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA エージェントの作業を確認します。
4. 完了後、報告を読みます。

## まとめと次のステップ

ワークフローに専門的な役割を追加し、その作業を確認しました。カスタムエージェントが指示、スキル、MCP ツールと連携する方法を調べ、QA プロファイルを作成して、フィルター機能の Issue に対する報告を確認しました。

実装、スキルの更新、QA プロファイル、テスト、検証結果がそろいました。次は[機能 PR を作成し、Agent Merge を使います][next-lesson]。

## 参考資料

- [Copilot CLI 向けカスタムエージェントを作成する][create-agents]
- [カスタムエージェントの設定][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
