---
title: "レッスン 6 - Playwright MCP による機能の検証"
description: "Copilot CLI で Playwright MCP を確認または設定し、ブラウザーからフィルター機能を調べます。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

コードを書く以外にも、データや外部サービスを扱い、Copilot で利用できる自動化を追加する必要があります。MCP サーバーを使うと、Copilot CLI に組み込まれていないツールやサービスを利用できます。

このレッスンでは、次のことを行います。

- Model Context Protocol (MCP) と Copilot CLI での利用方法を理解します。
- Playwright MCP サーバーがまだ利用できない場合は追加します。
- エージェントにブラウザーを操作させ、フィルター機能を確認します。

## シナリオ

ユニットテストやエンドツーエンドテストは重要ですが、UI の変更を検証するには、実際に UI を操作する必要があります。Copilot に利用者と同じようにサイトを使わせ、変更が期待どおりに動作するか確かめます。

## Model Context Protocol (MCP) とは

[Model Context Protocol (MCP)][mcp-blog-post] は、AI エージェントが外部のツールやサービスと通信するための仕組みです。MCP を使うと、AI エージェントは最新の情報にアクセスしたり、ユーザーに代わって操作を行ったりできます。

ツールやリソースには、AI エージェントと外部サービスの橋渡しをする MCP サーバーを通じてアクセスします。各 MCP サーバーは、エージェントが利用できる異なるツールとリソースを提供します。

よく使われる MCP サーバーには、次のものがあります。

- **[GitHub MCP Server][github-mcp]**: GitHub リポジトリ、Issue、プルリクエストを管理する API にアクセスします。
- **[Playwright MCP Server][playwright-mcp-server]**: Playwright を使ったブラウザー自動化機能を提供します。

ほかにもさまざまな MCP サーバーがあります。GitHub は、見つけやすさとエコシステムへの貢献を促進するために [MCP registry][mcp-registry] をホストしています。

> [!CAUTION]
> MCP サーバーは、プロジェクト内のほかの依存関係と同様に扱ってください。利用前にソースコードを確認し、発行元を検証して、セキュリティへの影響を検討します。

## Playwright MCP サーバーを追加する

Playwright MCP サーバーがまだ利用できない場合は、Copilot が Web サイトを操作できるよう追加します。

> [!NOTE]
> Copilot CLI ですでに Playwright MCP が設定されている場合は、この手順を省略して次のセクションに進みます。

1. Codespace に戻ります。
2. Copilot CLI で次のコマンドを入力し、MCP サーバー追加ダイアログを開きます。

   ```plaintext
   /mcp add
   ```

3. 名前として `playwright` と入力し、<kbd>Tab</kbd> を押します。
4. サーバーの種類が **STDIO** であることを確認し、<kbd>Enter</kbd>、次に <kbd>Tab</kbd> を押します。
5. **Command** ダイアログに次を貼り付けます。

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. <kbd>Control</kbd>+<kbd>S</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) を押して、新しい MCP サーバーを保存します。
7. <kbd>Esc</kbd> を押して MCP ダイアログを閉じます。

## Playwright を使って Copilot に機能を調べてもらう

以前は機能が期待どおりに動作するか手動で確認しました。今度は Copilot で利用できる Playwright MCP サーバーを使って同じ確認を行います。

1. 次のプロンプトを使い、Playwright MCP サーバーで機能を検証するよう Copilot に依頼します。

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> 通常は MCP サーバーを明示しなくても Copilot が適切なサーバーを判断します。ただし、使用するサーバーが分かっている場合は指定すると、結果の一貫性を高め、トークンを節約できます。

2. Copilot がブラウザーを操作して機能を確認する手順を追います。
3. 結果を読み、すべて期待どおりに動作していることを確認します。

Copilot はアプリを起動し、Playwright でサイトを操作し、サーバーを停止して結果を報告します。

## まとめと次のステップ

Copilot CLI から Playwright MCP サーバーを使い、実際のブラウザーで機能を確認しました。MCP と Copilot CLI での利用方法を学び、サーバーを追加して、エージェントにブラウザーを操作させました。

次は、スキルとブラウザーツールを専門的な役割にまとめる[カスタム QA エージェントを作成します][next-lesson]。

## 参考資料

- [MCP が注目されている理由][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [Copilot CLI に MCP サーバーを追加する][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
