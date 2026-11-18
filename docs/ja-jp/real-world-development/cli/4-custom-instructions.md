---
title: "レッスン 4 - カスタム指示による Copilot のガイド"
description: "リポジトリの指示を確認してドキュメント標準を追加し、フィルター機能のコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使うときは、コンテキストが重要です。特定の方法でタスクを実行したい場合は、Copilot がそのガイダンスを参照できるようにします。[指示ファイル][instruction-files]を使うと、必要なコードだけでなく、その構成方法も伝えられます。フィルター機能を構築したので、Copilot が使った指示を確認し、ドキュメント標準を追加して、コードに適用します。

このレッスンでは、次のことを行います。

- リポジトリの指示とパスを指定した指示ファイルがエージェントに適用される方法を確認します。
- コーディング標準を守るために指示ファイルを更新します。
- 指示ファイルがコードに与える影響を確認します。

## シナリオ

Tailspin Toys には開発の進め方に関するガイドラインがあります。

- コメントではコードを言い換えるのではなく、意図や自明でない決定を説明します。
- `db/` と `src/lib/` のエクスポート関数は、目的、パラメーター、戻り値を TSDoc/JSDoc で説明します。`db` 引数を注入する場合は、その説明も含めます。
- 再利用可能な Astro コンポーネントには `Props` の契約を記載し、関連するコードの変更時にコメントも更新します。
- 既存の書式設定と lint のガイダンスを維持します。

指示ファイルを使い、これらの開発方針に沿って Copilot が作業できるよう必要な情報を提供します。

## 指示ファイル

カスタム指示は、コーディングスタイルや要件を Copilot に伝えます。コーディング規約、ライブラリ、コメントの書き方などを指定して、適切な提案やコードを生成するよう導けます。リポジトリ全体に適用する指示も、特定のファイル種別に適用する指示も作成できます。

指示ファイルには次の2種類があります。

- `.github/copilot-instructions.md` は、リポジトリへのすべての要求に適用される単一の指示ファイルです。ほとんどの要求に関係するプロジェクト情報を記載します。
- `.github/instructions/*.instructions.md` は、言語、ファイル種別、タスクに関するガイダンスを記載します。

> [!NOTE]
> ほかの指示形式とサポート状況は環境によって異なります。形式を利用する前に、[カスタム指示のサポートに関するリファレンス][custom-instructions-support]を確認してください。

## プロジェクトのカスタム指示を確認する

スタータープロジェクトには、すでに指示ファイルが含まれています。変更前に内容を確認して、指示の効果を把握しましょう。

1. Codespace に戻ります。
2. Codespaces エディターで (ターミナルではなく) `.github/copilot-instructions.md` を開きます。
3. プロジェクトの概要とコーディングガイダンスを確認します。この指示は、リポジトリ内で Copilot を使うすべての作業に適用されます。
4. `.github/instructions` フォルダーを開き、Astro、Drizzle データ層、テストなどの指示を確認します。
5. `.github/instructions/unit-tests.instructions.md` を開き、適用対象のファイルを指定する `applyTo` フロントマターを確認します。
6. `.github/instructions/drizzle.instructions.md` を開き、ほかの指示ファイルや既存のプロジェクトファイルへのリンクを確認します。指示を再利用しやすい小さなファイルに分け、Copilot が参考にできる例を示せます。

## チームの方針に合わせて指示ファイルを更新する

既存の指示は出発点として十分ですが、TypeScript に新しく追加するコードに TSDoc コメントを含める必要があります。コアの `copilot-instructions.md` を更新しましょう。

1. `.github/copilot-instructions.md` の **Code formatting guidance** セクションを探します。35行目前後にあります。
2. 最後の項目として、次の Markdown を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

変更は自動的に保存されます。

## 更新したガイダンスを使う

Copilot CLI は会話の開始時にリポジトリの指示を読み込みます。フィルター機能のコンテキストを保ったまま新しい指示を適用するため、会話を終了して再開します。

1. フィルター機能の会話が開いている場合は `/exit` を入力します。Copilot CLI は会話を自動的に保存します。
2. リポジトリのルートで `game-filters-cli` ブランチに切り替えてから、保存済みの会話を再開します。

   ```bash
   copilot --resume
   ```

   選択画面が表示されたらフィルター機能の会話を選び、`game-filters-cli` ブランチがチェックアウトされていることを確認します。

3. Copilot に、更新したガイダンスを適用するよう依頼します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力し、変更された TypeScript ファイルを確認します。新しい TSDoc コメントがコードを正確に説明していることを確認します。

## まとめと次のステップ

Copilot CLI が指示ファイルからコンテキストを取得する方法を確認し、新しい標準をフィルター機能に適用しました。リポジトリの指示とパスを指定した指示ファイルを確認し、指示ファイルを更新して、コードへの影響を確かめました。

次は、[再利用可能な quality-checks スキルをカスタマイズして実行します][next-lesson]。

## 参考資料

- [Copilot CLI にカスタム指示を追加する][instruction-files]
- [カスタム指示のサポート][custom-instructions-support]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
