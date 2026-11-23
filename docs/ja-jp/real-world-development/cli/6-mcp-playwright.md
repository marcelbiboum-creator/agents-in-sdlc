---
title: "レッスン 6 - Playwright MCP による機能の検証"
description: "Copilot CLI で Playwright MCP を確認または設定し、ブラウザーでフィルター機能を調査します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

コードを書くことだけが重要なのではありません。データや外部サービスを扱うことも必要で、Copilot が利用できる自動化を追加する必要があります。ここで MCP server が役立ちます。MCP server は Copilot の組み込み機能を超えてツールとサービスを追加します。

このレッスンでは、次の内容を学習します。

- Model Context Protocol (MCP) と Copilot CLI の使用方法を理解する。
- Playwright MCP server が利用可能でない場合は追加する。
- エージェントにブラウザーを操作させ、フィルター機能を確認させる。

## シナリオ

単体テストとエンドツーエンド テストは重要ですが、UI の更新を検証するには実際に UI を操作する必要があります。Copilot が作業中の Web サイトをユーザーと同じように操作できるようにし、更新が期待通りに動作する信頼性を高めます。

## Model Context Protocol (MCP) とは

[Model Context Protocol (MCP)][mcp-blog-post] は、AI エージェントが外部ツールやサービスと通信する方法を提供します。MCP を使うと、AI エージェントは外部ツールやサービスにリアルタイムでアクセスし、代わりに操作を実行できます。

これらのツールとリソースには MCP server を通じてアクセスします。MCP server は、AI エージェントと外部ツールやサービスの橋渡しをします。MCP server ごとに、エージェントが利用できるツールやリソースが異なります。

よく使われる既存の MCP server は次のとおりです。

- **[GitHub MCP server][github-mcp]:** GitHub リポジトリ、Issue、pull request を管理する API にアクセスします。
- **[Playwright MCP server][playwright-mcp-server]:** Playwright を使ってブラウザーを自動操作します。

ほかにも多くの MCP serverがあります。GitHub の [MCP registry][mcp-registry]で検出性とエコシステムへの貢献を確認できます。

> [!CAUTION]
> MCP server はプロジェクトのほかの依存関係と同じように扱ってください。使用前にソース コードを確認し、公開元を検証し、セキュリティ上の影響を検討してください。

## Playwright MCP server を追加する

Playwright MCP server が利用可能でない場合は追加し、Copilot がユーザーと同じように Web サイトを操作できるようにします。

> [!NOTE]
> Playwright MCP が Copilot CLI にすでに設定されている場合は、セットアップ手順を省略して次のセクションに進んでください。

1. Codespace に戻ります。
2. Copilot CLIで次のコマンドを入力し、MCP server の追加ダイアログを開きます。

   ```plaintext
   /mcp add
   ```

3. 名前に `playwright` を入力し、<kbd>Tab</kbd> を押します。
4. サーバー種別が **STDIO** であることを確認し、<kbd>Enter</kbd> を押してから <kbd>Tab</kbd> を押します。
5. 次のコマンドを **Command** ダイアログに貼り付けます。

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. <kbd>Control</kbd>+<kbd>S</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) を押して、新しい MCP server を保存します。
7. <kbd>Esc</kbd> を押して MCP ダイアログを終了します。

## Copilot に Playwright を使って機能を確認させる

これまで機能が期待通りに動作することを手動で確認しました。次は、Copilot が利用できる Playwright MCP server を使って同じ確認を行います。

1. 次のプロンプトを使い、Copilot に Playwright MCP server を使った機能検証を依頼します。

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> MCP server を明示的に指定する必要はありません。Copilot は通常、必要なツールを判断します。ただし、使用するツールがわかっている場合は、方向を示すことがより一貫した結果につながり、トークンも節約できます。

2. Copilot がブラウザーで実行する各ステップを確認します。
3. レポートを読み、すべてが期待通りに動作することを確認します。

Copilot はサーバーを起動し、Playwright を使って Web サイトを操作し、サーバーを停止し、レポートを返します。

## まとめと次のステップ

Copilot CLI から Playwright MCP server を使って、実際のブラウザーで機能を確認しました。振り返ると、次の作業を行いました。

- Model Context Protocol (MCP) と Copilot CLI の使用方法を理解した。
- Playwright MCP server が利用可能でない場合は追加した。
- エージェントにブラウザーを操作させ、フィルター機能を確認させた。

次は、スキルとブラウザー ツールを専門的な役割にまとめる [QA カスタム エージェントを作成][next-lesson]します。

## リソース

- [MCPとは、なぜ話題なのか][mcp-blog-post]
- [Microsoft Playwright MCP server][playwright-mcp-server]
- [Copilot CLI に MCP server を追加する][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
