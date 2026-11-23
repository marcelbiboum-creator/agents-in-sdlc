---
title: "レッスン 1 - GitHub Copilot CLI のインストール"
description: "Codespace に Copilot CLI をインストールして認証し、作業環境を確認し、用意されたフィルター Issue を見つけます。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] は、ターミナルでコードベースを探索し、コードを生成し、コマンドを実行し、外部ツールと対話できるエージェント型コーディング アシスタントです。作業の引き継ぎ、変更の依頼、集中状態の維持ができます。最初のステップはツールをインストールすることです。

このレッスンでは、次の内容を学習します。

- npm を使って GitHub Copilot CLI をインストールする。
- GitHub アカウントで認証する。
- ワークショップ リポジトリを信頼し、簡単な会話を試す。
- 内蔵の GitHub MCP server を使ってフィルター Issue を見つける。

## シナリオ

チームは、増え続けるバックログに対応するため AI エージェントを導入し始めています。Copilot CLI は、開発者がすでに多くの時間を使うターミナルにその機能を提供します。このレッスンでは、インストールと認証を完了し、ワークショップの残りの作業を開始できる状態にします。

## Copilot CLI をインストールする

Copilot CLI は [npm][install-cli]、WinGet、Homebrew でインストールできます。GitHub Codespaces には Node.js があらかじめインストールされているため、npm を使用します。

1. Codespace に戻り、ターミナルを開きます。
2. Node.js がインストールされ、必要なバージョンを満たしていることを確認します。

   ```bash
   node --version
   ```

   バージョン 24 以上が表示されれば十分です。

3. Copilot CLI をグローバルにインストールします。

   ```bash
   npm install -g @github/copilot
   ```

4. インストールを確認します。

   ```bash
   copilot --version
   ```

   バージョン番号が表示されれば成功です。

## GitHub で認証する

初回起動時、Copilot CLI は GitHub アカウントでの認証を求めます。

1. Copilot CLI を起動します。

   ```bash
   copilot
   ```

2. 認証を求められたら、デバイスコードの手順に従って Copilot CLI を認証し、承認します。
3. Copilot CLI に次のプロンプトが表示されます。

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. パスが Tailspin Toys リポジトリであることを確認し、**Yes, and remember this folder for future sessions** を選択して「はい」と回答します。

> [!NOTE]
> Codespace では、GitHub セッションを通じて認証済みの場合があります。Copilot CLI が認証を求めずに起動した場合は、そのまま進められます。

## 作業環境を確認する

通常のシェル プロンプトから実行するコマンドは Codespace に直接送られます。Copilot CLI を起動すると、自然言語の入力はエージェントに送られ、スラッシュコマンドで会話を操作します。

1. `/model` を入力し、矢印キーで **Auto** を選択し、<kbd>Enter</kbd> を押してからもう一度押して確認します。
2. `/help` を入力して、インストール済みバージョンで使用できるコマンドを確認し、<kbd>Esc</kbd> を押してヘルプ画面を閉じます。
3. 簡単な質問をして、Copilot が動作することを確認します。

   ```plaintext
   What are the key files in this project?
   ```

4. 応答を読み、回答前に Copilot がリポジトリを調査することを確認します。
5. `/mcp list` を入力し、内蔵の GitHub MCP server が利用可能であることを確認します。
6. Copilot にフィルター Issue を見つけるよう依頼します。

   ```plaintext
   Using GitHub MCP, find the issue in this repository titled "Allow users to filter games by category and publisher." Give me its URL and a short summary. Don't change anything.
   ```

7. URL を開いて Issue を読みます。簡単な最初の変更を完了した後、この Issue を使用します。

> [!TIP]
> 通常の Copilot CLI セッションは、ターミナルで現在チェックアウトされているブランチで動作し、worktree を自動作成しません。変更ごとにフィーチャー ブランチを作成します。

## ワークショップ用ショートカットを使用する

Copilot CLI は通常、確立された権限の範囲外でツールを使用する前に確認を求めます。このワークショップでは、Codespace 内の承認プロンプトをなくす、ユーザー承認済みのショートカットである `--yolo` を使って再起動します。

> [!CAUTION]
> `--yolo` を指定すると、完全な自動権限 (`--allow-all-tools`、`--allow-all-paths`、`--allow-all-urls`) が有効になります。Codespace または VM のような隔離された環境だけで使用し、日常の開発で既定としてエイリアスにしないでください。詳細は [ツールの使用を許可または拒否する][allow-all-warning]を参照してください。

このワークショップでは、`--enable-all-github-mcp-tools` により、後続のレッスンで Issue と pull request を扱う読み取り/書き込み GitHub MCP ツールを有効にします。Codespace はローカル コンピューターへのアクセスを制限していますが、認証済みの GitHub リソースは実環境です。公開またはマージする前に変更を確認してください。

1. `/exit` で Copilot CLI を終了します。
2. リポジトリのルートから再起動します。

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. プロジェクトについて別の簡単な質問をして会話を確認し、`/exit` で終了します。

Copilot は会話を自動保存します。指示を変更したりエージェントを追加したりした場合は、`copilot --resume` を使用して同じフィーチャー会話とブランチに戻ります。

## まとめと次のステップ

おめでとうございます。このレッスンでは、次の作業を完了しました。

- npm を使って GitHub Copilot CLI をインストールした。
- GitHub アカウントで認証した。
- ワークショップ リポジトリを信頼し、簡単な会話を試した。
- 内蔵の GitHub MCP server を使ってフィルター Issue を見つけた。

次は、[最初の対象を絞った変更を開始][next-lesson]し、Copilot CLI を使ってゲームカードに星評価を表示します。

## リソース

- [GitHub Copilot CLI のインストール][install-cli]
- [GitHub Copilot CLI の概要][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
