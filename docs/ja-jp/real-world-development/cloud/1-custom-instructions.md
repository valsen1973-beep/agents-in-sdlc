---
title: "レッスン 1 - カスタム指示 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。特定の方法でタスクを実行したい場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。[指示ファイル][instruction-files]を使うと、コード生成で「何を」するかだけでなく、「どのように」実行するかも Copilot に伝えられます。

この演習では、次のことを行います。

- リポジトリのカスタム指示とパスを指定した指示ファイルを通じて、プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント標準が Copilot に伝わる方法を確認します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加します。

> [!NOTE]
> VS Code や CLI のワークショップとは異なり、ここではプロンプトの実行前後を比較しません。Copilot cloud agent は GitHub Issue に対して非同期で作業するため、リアルタイムで並べて効果を示すのが難しいためです。このワークショップの後半で cloud agent が作成したプルリクエストをレビューするときに、指示ファイルの影響を確認します。

## 指示ファイル

### シナリオ

Tailspin Toys には、開発の進め方に関するガイドラインがあります。たとえば、次のような要件です。

- データ層には必ずユニットテストを用意します。
- UI はダークモードにし、現代的な見た目にします。
- TSDoc のドキュメントコメントをコードに追加します。
- 各ファイルの先頭に、ファイルの役割を説明するコメントブロックを追加します。

指示ファイルを使い、Copilot がこれらの開発方針に沿ってタスクを実行するために必要な情報を提供します。

### カスタム指示

カスタム指示は、コーディングスタイルや要件に関するコンテキストと希望を Copilot に伝えます。これにより、より適切な提案やコードを生成するよう導けます。コーディング規約、ライブラリ、コードに含めるコメントなどを指定できます。リポジトリ全体に適用する指示も、特定のファイル種別に適用する指示も作成できます。

指示ファイルには次の2種類があります。

- `.github/copilot-instructions.md` は、リポジトリに対する**すべての**要求とともに Copilot に送信される単一の指示ファイルです。技術スタック、開発対象の概要、ベストプラクティス、全般的なガイダンスなど、ほとんどの Copilot Chat または CLI 要求に関係する情報を記載します。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイル種別に使う指示ファイルです。TypeScript や Astro などの言語、UI コンポーネントの作成、ユニットテストの作成といった作業向けのガイダンスを記載できます。

> [!NOTE]
> IDE では、指示ファイルは Copilot Chat によるコード生成にのみ使用され、コード補完や次の編集候補には使用されません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、コード生成時にリポジトリレベルの指示と `applyTo` フロントマターが設定された `*.instructions.md` ファイルの両方を使用します。
>
> Copilot は AGENTS.md や CLAUDE.md など、ほかの形式の指示ファイルも[サポートしています][custom-instructions-support]。

### 指示ファイルを管理するためのベストプラクティス

このワークショップでは指示ファイルの作成方法を詳しく扱いませんが、サンプルプロジェクトには代表的な方法が含まれています。基本的には、次の点を意識します。

- `copilot-instructions.md` には、開発対象の説明、プロジェクト構成、全体に適用するコーディング標準など、プロジェクトレベルのガイダンスを記載します。
- `*.instructions.md` は、ユニットテスト、Astro コンポーネント、データ層といったファイル種別や、特定のタスク向けに使用します。
- 自然な言葉で、明確なガイダンスを書きます。コードの良い例と避けるべき例も示します。

指示ファイルの作り方や AI の使い方に唯一の正解はありません。プロジェクトで試しながら、最適な方法を見つけてください。

> [!TIP]
> GitHub Copilot を使うプロジェクトには、十分な指示ファイルを用意することをお勧めします。このプロジェクトには、[UI 更新用の指示][ui-instructions]や [Astro 用の指示][astro-instructions]などがあります。
>
> Copilot に指示ファイルを作成させることもできます。設定方法は利用する環境によって異なります (例: VS Code の **Configure Chat → Generate Agent Instructions**、Copilot CLI の `/init`)。このワークショップでは、必要に応じて各環境での方法を説明します。
>
> テンプレートやひな形を探す場合は、指示ファイル、カスタムエージェントなどを集めた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

このリポジトリには、中心となる `copilot-instructions.md` と、タスク別の `*.instructions.md` ファイルがあります。エディターまたは GitHub の Web UI で確認してください。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡単な説明と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** にある **GitHub Actions Workflows** の指針を含め、これらは Copilot を使うあらゆる作業に適用されます。
3. `.github/instructions` フォルダーを開いて内容を確認します。Astro ファイル、Drizzle データ層、テストなどの指示があります。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドは、指示を適用するファイルを決めるリポジトリルート相対の glob です。ここでは、`**/*.test.ts` に一致する TypeScript のテストファイルが対象になります。
5. ユニットテスト作成に関する指示を確認します。
6. `.github/instructions/drizzle.instructions.md` を開き、末尾までスクロールします。`unit-tests.instructions.md` などの指示ファイルや、プロジェクト内の既存ファイルへのリンクがあります。大きな指示を再利用しやすい小さなファイルに分け、Copilot が参照できる例を示せます。ここにあるパスはリポジトリルートではなく、指示ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトのコーディング標準が記載されていますが、コード内のドキュメントに関する要件はまだありません。次の手順で、TSDoc のドキュメントコメントとファイルヘッダーの規則を追加します。

## リポジトリ標準を追加する

この演習では、コード内のドキュメントとして TSDoc コメントとファイル先頭のコメントヘッダーを追加する、プロジェクト全体のルールを設定します。後の演習で cloud agent に Issue を割り当てると、この指示が使われます。

編集の前に、作業用のブランチを作成します。cloud agent は Issue の対象ブランチにある指示を読み込みますが、変更を整理してコミットするため、ここではブランチを使います。

1. Codespace のターミナルで、新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`.github/copilot-instructions.md` は Copilot にプロジェクトレベルの情報を伝えるファイルです。コーディング標準を記載して、コード提案の改善に役立てましょう。

1. `.github/copilot-instructions.md` を開き直します。
2. 27行目前後にある **Code formatting requirements** セクションを探します。現時点ではコード内のドキュメントに関する規則がないため、生成されたヘルパーにドキュメントコメントがありません。
3. 既存の標準の直後に、次の Markdown を追加します。これにより、Copilot にファイルヘッダーと TSDoc コメントの追加を指示できます。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで確認したように、指示ファイルはリポジトリ全体に適用する `.github/copilot-instructions.md` と、言語、ファイル種別、タスクに使う `*.instructions.md` のどちらにも作成できます。今回追加したドキュメントコメント規則のようなプロジェクト全体の標準には、リポジトリレベルのファイルが適しています。

## 指示の変更をコミット、プッシュ、マージする

cloud agent は、Issue が対象とするブランチにある指示ファイルを読み込みます。次の演習で Copilot に Issue を割り当てると、`main` からブランチが作られます。そのため、指示の変更を `main` にマージしておく必要があります。

1. 変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` に向けたプルリクエストを作成してマージします。次の演習で Issue を割り当てるとき、cloud agent がこの指示を読み込めるようになります。

> [!TIP]
> このワークショップでは、ブランチを使わず `main` に直接作業してもかまいません。実際のプロジェクトでの手順に近づけるため、ここではブランチを使っています。

## まとめと次のステップ

このプロジェクトの指示ファイルから Copilot がコンテキストを取得する方法を確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。このワークショップの残りで cloud agent が作成するプルリクエストをレビューするときに、この標準が反映されているか確認します。

次は、[最初の Issue を Copilot cloud agent に割り当てます][next-lesson]。

## 参考資料

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Copilot 向けのカスタム指示を改善する5つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
[awesome-copilot]: https://github.com/github/awesome-copilot
