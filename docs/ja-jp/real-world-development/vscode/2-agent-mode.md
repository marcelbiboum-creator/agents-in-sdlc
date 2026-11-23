---
title: "演習 2 - Copilot エージェント モードで新機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

アプリケーションの小さな更新でも、複数ファイルの変更やテスト実行が必要です。開発者は必要なファイルを探し、変更し、テストして、デバッグし、見落としたファイルを見つけて再度更新します。この反復作業を Copilot エージェント モードで効率化できます。

Copilot エージェント モードは、IDE 内でより自律的に動作します。開発者と同様に、既存のプロジェクト構造を調査し、必要な更新を行い、テストなどのタスクを実行し、発見した問題を修正します。

> [!NOTE]
> 名前は似ていますが、エージェント モードと cloud agent は異なる体験向けです。エージェント モードは IDE 内で迅速なフィードバックを得られます。cloud agent は Issue と pull request を介してチームメンバーと協働する非同期のペアプログラマーです。

この演習では、次のことを学びます。

- Copilot エージェント モードがプロジェクトを調査し、関連ファイルを特定し、整合性のある変更を行う方法。
- GitHub Copilot エージェント モードが UI とデータ層にまたがる新機能を実装する方法。
- マージ前に Copilot が生成した変更とテストをレビューする方法。

## シナリオ

ゲーム一覧が増えているため、ユーザーがカテゴリーとパブリッシャーで絞り込めるようにします。前の演習でパブリッシャー ヘルパーを追加済みなので、エージェント モードで残りのデータ層、UI、テスト作業を完了します。

## Tailspin Toys Web サイトを実行する

変更前に Web サイトを確認し、現在の機能を理解します。

Tailspin Toys は、開発者テーマのボードゲーム向けクラウドファンディング プラットフォームです。ゲーム一覧と詳細を表示します。単一の Astro アプリで、ビルド時に静的 HTML を生成します。ページは Drizzle ORM を通じてフロントマターからローカル SQLite データベースに直接問い合わせます。再利用可能なデータアクセスヘルパーは`src/lib/`にあり、相互作用は標準 DOM API を使う小さな Astro`<script>`で追加します。

### Web サイトを起動する

1. Codespace に戻り、前の演習後に`main`にいることを確認します。
2. <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押してターミナルを開きます。
3.フィルター作業用のブランチを作成します。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次を実行して Web サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro サーバーが準備できると、次のような URL を含むメッセージが表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321`を開くダイアログが表示されたら、**x**を選択して閉じます。

5. Macは<kbd>Command</kbd>、Windows/Linuxは<kbd>Ctrl</kbd>を押しながら、ターミナルの`http://localhost:4321`を選択します。

> [!NOTE]
> Codespaceでは、ターミナルの localhost リンクを選択すると、`https://<codespace-name>-4321.app.github.dev/`へリダイレクトされ、codespaceでホストされた Web サーバーへ接続します。

### Web サイトを確認する

主な機能は次のとおりです。

- **Home Page:** タイトル、画像、説明付きのボードゲーム一覧を表示します。
- **Game Details Page:** ゲームを選択すると、タイトル、説明、パブリッシャー、カテゴリーを含む詳細ページを表示します。

## Copilot でバックログを確認する

> [!TIP]
> **Copilot Chat を開く**
>
> Codespaceに戻り、Copilot Chat パネルを開き、**New Chat**で新しい会話を開始します。

テンプレート作成時にバックログ Issue が登録されています。Copilot に一覧を依頼します。

1. Chat ビューのエージェント ピッカーから**Agent**を選択します。エージェントはファイル間で計画・実装し、ターミナル コマンドとツールを実行します。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

2. 利用可能なモデル一覧から**Claude Sonnet 4.5**を選択します。

> [!CAUTION]
> ワークショップの作成時に Claude Sonnet 4.5 を使用しましたが、特定のモデルを推奨するものではありません。LLMは確率的に動作するため、提案がワークショップの説明と完全に一致しない場合があります。

> [!NOTE]
> LLMは確率的なため、Copilot が異なる MCP コマンドを使用する場合がありますが、タスクは完了できます。

3. 次のプロンプトを Copilot に送信します。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. コマンドの実行に**Continue**を選択します。
5. 生成された Issue 一覧を確認します。

Copilot はユーザーにとって有用度に基づいて項目を優先順位付けできることを確認します。

## 指示ファイルを確認する

エージェントにコード生成を依頼する前に、コンテキストを提供する指示ファイルを確認します。Web サイトへの機能追加方法を示す[UI][ui-instructions]指示ファイルを使用します。

1. Codespaceで`.github/instructions/ui.instructions.md`に移動します。
2. 概要、コンポーネント設計、テスト、アクセシビリティの原則、Astro、Tailwind CSS、Drizzleなどの特定の指示ファイルへのリンクを確認します。

> [!TIP]
> 指示ファイルはほかの指示ファイルやプロジェクト ファイルを参照できます。パスは指示ファイルの場所からの相対パスです。

## フィルター機能を実装する

フィルターを完成させるには、少なくとも次の3種類の更新が必要です。

- データ層 (`src/lib/`) のフィルター ロジックを追加または改善する。
- フィルター動作のテストを追加または更新する。
- ゲーム一覧ページにフィルター UI を追加または更新する。

マージ前にテストが実行され、成功する必要があります。Copilot エージェント モードでこれらのタスクを実行できます。

1. 現在の会話を継続するか、**New Chat**を選択して新しい会話を開始します。
2. **Add Context**、**Instructions**、**ui**の順に選択し、UI 指示ファイルを追加します。

   ![UI 指示ファイルの選択例](../../../_images/ex3-select-instructions-file.png)

3. エージェント ピッカーで**Agent**を選択したままにします。
4. モデルで**Claude Sonnet 4.5**を選択したままにします。
5. バックログの関連 Issue に基づいて機能を実装するよう Copilot に依頼します。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調査し、関連ファイル、データ層ヘルパー、UI、テストを特定し、変更とテスト実行を開始します。

   ![Copilot がプロジェクトファイルを調査する画面](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot は調査、ファイル変更、テスト実行などを行います。処理には数分かかる場合があります。作業中はエディターに**Keep**と**Undo**が表示されます。完了時まで選択する必要はありません。

7. Copilot のプロンプトに従い、**Continue**を選択してテストを実行します。

   ![テスト実行の確認ダイアログ](../../../_images/ex3-agent-mode-run-tests.png)

8. 処理中にテストが失敗する場合があります。Copilot はコード生成とテストを反復し、エラーがなくなるまで作業します。

   ![Copilot エージェント モードの完全なチャット セッション](../../../_images/ex3-agent-mode-proposed-changes.png)

9.生成されたコードを確認します。

> [!CAUTION]
> Copilot または AIツールが生成したコードは、必ずレビューしてください。

10.実行中の Web サイトをブラウザーで開き、新機能を確認します。
11.動作とコードを確認したら、Copilot Chatで**Keep**を選択します。

## まとめと次のステップ

GitHub Copilot エージェント モードを使って Tailspin Toys の新機能を追加する方法を確認しました。

- エージェント モードは UI とデータ層にまたがる新機能を実装できる。
- プロジェクトを調査し、関連ファイルを特定し、整合性のある変更を行える。
- マージ前に Copilot が生成した変更とテストをレビューする必要がある。

次は、[Playwright MCP serverでフィルター機能をテスト][next-lesson]し、pull requestを作成します。

### ボーナス演習 - ページネーションを実装する

ゲーム一覧が増えると、ページネーションが必要になります。この演習で学んだスキルを使い、ページネーションを実装するよう Copilot に依頼します。

- 既存の指示ファイルなど、既存のベストプラクティスに従うこと。
- ページサイズをユーザーに選択させるか、固定するかを決めること。
- 実装したい結果を明確にするプロンプトを書くこと。
- 必要に応じて Copilot に変更を依頼し、コンテキストを追加して反復すること。

## リソース

- [Copilot ask、edit、agent モードの違いと使い分け][choose-mode]
- [VS Code のエージェント モード][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
