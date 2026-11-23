---
title: "レッスン 2 - 星評価の追加で小さな成果を得る"
description: "Copilot CLI を使ってゲームカードに小規模な変更を加え、転送されたブラウザーで確認して、最初の pull request としてマージします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI をインストールして会話を試したので、次はプロジェクトに最初の変更を加えます。変更は小規模にします。ゲームのデータにはすでに星評価がありますが、ホームページのゲームカードにはまだ表示されていません。エージェントに表示を依頼し、変更をレビューして、最初の pull request としてマージします。

このレッスンでは、次の内容を学習します。

- フィーチャー ブランチで対象を絞った Copilot 会話を開始する。
- エージェントに小規模な変更を依頼する。
- `/diff` を使って変更をレビューする。
- アプリを起動し、転送されたブラウザーで変更を確認する。
- 最初の pull request を作成してマージする。

## シナリオ

Tailspin Toys の各ゲームには星評価があり、ゲーム詳細ページにはすでに表示されています。一方、ホームページのゲームカードには、タイトル、カテゴリー、パブリッシャー、説明しか表示されません。ウォームアップとして、エージェントに各カードへ既存の評価を表示させます。小規模で自己完結した、最初のセッションに最適な変更です。

## 会話の構造

**会話**とは、Copilot CLI でタスクを進める場です。Copilot app と異なり、通常の CLI 会話では専用の worktree を作成せず、ターミナルで現在チェックアウトされているリポジトリと Git ブランチを使用します。保存された会話を使えば、後で同じ会話に戻れます。ファイルとブランチはディスク上の通常の Git 状態として保持されます。

会話では、プロンプトとエージェントの応答、調査やファイル編集時のツールアクティビティ、`/diff` で確認できる変更という 3 要素を確認できます。

## 会話を開始して変更を依頼する

新しい会話を開始し、機能の実装を始めます。

1. Codespace に戻ります。
2. 前からターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
3. 開いていない場合は、次のコマンドで Copilot を起動します。

   ```bash
   copilot --yolo
   ```

4. `/new` スラッシュコマンドを使って新しいセッションを開始し、<kbd>Enter</kbd> を押します。
5. 次のプロンプトを使って変更を依頼します。

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot はプロジェクトを調査し、ゲーム詳細の表示に使用されるファイルを特定し、必要なコードを作成します。これで Copilot CLI を使って新機能を追加できました。

## 差分をレビューする

生成 AI が作成した変更は、どれほど小さくても、マージ前にレビューします。

1. `/diff` を入力し、変更されたファイルをすべて確認します。
2. 評価がある場合は数値の評価がゲームカードに表示され、`starRating` が `null` の場合は `No rating yet` が表示されることを確認します。
3. テストが両方の状態をカバーしていることを確認します。
4. Copilot が実行したチェックの結果をレビューし、失敗があれば修正を依頼します。
5. レビューが完了したら、<kbd>Esc</kbd> を押して差分画面を終了します。

> [!NOTE]
> Copilot を含む生成 AI ツールは確率的に動作するため、実際のコードは上記と異なる場合があります。特定の実装ではなく、動作をレビューしてください。

## 変更を確認する

コードを読んだだけで動くと判断せず、ブラウザーで更新された UI を確認しましょう。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces がポート `4321` を利用可能だと通知したら、**Open in Browser** を選択します。
3. ゲームカードに評価が5点満点で表示されることを確認します。
4. Copilot に戻り、起動したサーバーを停止するよう依頼します。

   ```plaintext
   Stop the development server you started.
   ```

## 最初の pull request を作成してマージする

機能が完成したので、新しいコードをプロジェクトにマージする pull request (PR) を作成します。

1. デフォルト エージェントに変更のコミットを依頼します。

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. `/pr create` を入力します。Copilot CLI は、PR を作成するときに既存のコミットをプッシュし、PR の URL を表示します。
3. Mac は <kbd>Command</kbd>、Windows/Linux は <kbd>Ctrl</kbd> を押しながら、Copilot CLI が表示した URL を選択して PR を開きます。
4. 変更されたファイルとチェックをレビューします。
5. 問題がなければ、**Merge pull request** を選択し、マージを確定します。
6. Codespace に戻り、`/exit` を使って Copilot CLI を終了します。
7. ローカルの `main` を更新します。

   ```bash
   git checkout main
   git pull
   ```

## まとめと次のステップ

GitHub Copilot CLI を使って最初の変更を公開しました。具体的には、次の作業を行いました。

- 対象を絞った Copilot 会話をフィーチャー ブランチで開始した。
- ゲームカードに小規模な変更を加えるようエージェントに指示した。
- `/diff` を使って変更をレビューした。
- アプリを起動し、転送されたブラウザーで星評価を確認した。
- 最初の pull request を作成してマージした。

次は、[フィルター Issue を起点として Plan モードと Autopilot モードを使用][next-lesson]し、より大規模な機能を構築します。

## リソース

- [GitHub Copilot CLI の概要][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
