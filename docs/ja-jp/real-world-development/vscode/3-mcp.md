---
title: "演習 3 - Playwright MCP serverでフィルター機能をテストする"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: エージェント モード][previous-lesson] · [次のレッスン: カスタム エージェント →][next-lesson]

エージェント モードでフィルター機能を構築しました。pull requestを作成する前に、ブラウザーで実際に動作することを確認します。自分で操作する代わりに、**Playwright MCP server**を接続し、Copilot に実際のブラウザーを操作させてテストし、ブランチを公開して PR を作成します。

この演習では、次の内容を学習します。

- Model Context Protocol (MCP) と MCP serverが Copilot のツールを拡張する仕組みを理解する。
- Playwright MCP serverをワークスペースに追加する。
- Copilot にブラウザーでフィルター機能を手動テストさせる。
- ブランチを公開し、フィルター作業の pull requestを作成する。

## Model Context Protocol (MCP)とは

エージェント モードはエディターの外部に接続できるようになると、さらに強力になります。Model Context Protocol (MCP) は、エージェントが外部ツールやサービスと通信するための標準的な方法です。

![エージェント モードの内部と、MCP serverやVS Code拡張機能が提供するツールとの対話を示す図](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/)は、AI エージェントが外部ツールやサービスと通信する方法を提供します。MCP を使うと、エージェントは最新情報にリソース経由でアクセスし、ツール経由で操作を代行できます。

ツールとリソースは MCP serverを通じて利用されます。MCP serverは AI エージェントと外部ツールやサービスの橋渡しをします。GitHub MCP serverや npm パッケージなど、さまざまなツールセットを提供できます。

代表的な MCP serverは次のとおりです。

- **[GitHub MCP server](https://github.com/github/github-mcp-server):** GitHub リポジトリ、Issue、pull request を管理する API にアクセスします。
- **[Playwright MCP server](https://github.com/microsoft/playwright-mcp):** Playwright を使ってブラウザーを自動操作し、ページ移動、フォーム入力、ボタン選択を実行します。

GitHub はエコシステムで利用可能な MCP serverを確認できる[MCP registry](https://github.com/mcp)を提供しています。

> [!CAUTION]
> MCP serverはプロジェクトのほかの依存関係と同様に扱ってください。使用前にソース コードを確認し、公開元を検証し、セキュリティ上の影響を考慮してください。

## MCP構成を確認する

`.vscode/mcp.json`は、この VS Codeワークスペースで利用可能な MCP serverを構成します。

1. Codespaceで`.vscode/mcp.json`を開きます。
2. 次のように`github`serverが設定されているはずです。

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        }
      }
    }
    ```

この`github`エントリはプロジェクト テンプレートに含まれています。前の演習で Copilot がバックログ Issue を読めた理由です。リモート GitHub MCP serverをHTTP経由で接続し、Copilotがツールを初めて使用するときに GitHubで認証します。

## Playwright MCP serverを追加する

[Playwright MCP server][playwright-mcp-server]を追加して、Copilot が制御できるブラウザーを提供します。

1. `.vscode/mcp.json`に、次のように`github`と並んで`playwright`エントリを追加します。

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        },
        "playwright": {
          "command": "npx",
          "args": ["@playwright/mcp@latest", "--headless"]
        }
      }
    }
    ```

2. ファイルを保存します。

リモートの`github`serverと異なり、`playwright`はローカル serverです。VS Codeが`npx @playwright/mcp@latest`を実行して起動します。`--headless`はブラウザーをウィンドウなしで実行します。Codespaceにはデスクトップ画面がないため、この指定が必要です。

> [!NOTE]
> Tailspin Toys プロジェクトはすでにエンドツーエンドテストで Playwright を使用しています。ブラウザーが不足している場合は、Copilot に`npx playwright install chromium`を実行させて再試行します。

## serverを起動して信頼する

VS Codeは MCP serverをオンデマンドで起動します。Copilot が初めてツールを必要とする際、serverを起動し、信頼確認を求めます。

1. `.vscode/mcp.json`の`playwright`エントリ上部に表示される**Start**を選択し、構成を確認します。
2. 信頼確認が表示されたら、構成を確認して信頼を選択します。

手動起動は任意です。スキップしても、次の手順で Copilot がツールを初めて使用するときに serverが起動し、信頼確認を求めます。

## フィルター機能をテストする

Playwright MCP serverはCopilotに実ブラウザーを提供します。エージェントがページを開き、移動し、フィルターを適用し、結果を確認します。

次のプロンプトを送信します。

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot は Playwright MCP server経由でブラウザーを起動し、各ステップを実行し、結果を報告します。Issueの受け入れ基準と比較し、問題があればフォローアップするか修正を依頼します。

> [!NOTE]
> このテストではアプリが`http://localhost:4321`で実行されている必要があります。サーバーを停止していた場合は、プロンプト送信前に再起動してください。ブラウザーが不足している場合は、`npx playwright install chromium`を実行して再試行します。

## ブランチを公開して pull requestを作成する

機能が動作することを確認したら、チームがレビューできるよう pull request (PR) を作成します。最初に`filtering-vscode`ブランチを公開します。

1. Codespaceの**Source Control**パネルで変更を確認します。
2. **+**アイコンで変更をステージします。
3. **Sparkle**ボタンでコミット メッセージを生成します。
4. **Publish**を選択してブランチをリポジトリにプッシュします。

PR は github.com、GitHub CLI、Copilot Chatなど複数の方法で作成できます。Copilot Chatで作成する場合は、次の手順を実行します。

1. Copilot Chat パネルを開き、**New Chat**を選択します。
2. エージェント ピッカーで**Agent**を選択します。
3. 次のプロンプトを送信します。

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. 必要に応じて**Continue**を選択し、Copilot にタスクを許可します。
5. Copilot が Issue を検索し、正しい Issue と関連付けた PR を作成します。
6. Copilot が生成したリンクを選択して PR を確認します。まだマージしないでください。

## まとめと次のステップ

この演習では、次の内容を学習しました。

- Model Context Protocol (MCP) と MCP serverが Copilot のツールを拡張する仕組み。
- Playwright MCP serverをワークスペースに追加する方法。
- ブラウザーでフィルター機能を手動テストする方法。
- ブランチを公開し、フィルター作業の pull requestを作成する方法。

次は、アクセシビリティ レビューなどの対象を絞ったタスクを効率化する[カスタム エージェントを作成][next-lesson]します。

## リソース

- [MCPとは、なぜ話題なのか][mcp-blog-post]
- [Microsoft Playwright MCP server][playwright-mcp-server]
- [GitHub MCP server][github-mcp-server]
- [GitHub MCP registry][mcp-registry]
- [VS Codeの MCP server][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
