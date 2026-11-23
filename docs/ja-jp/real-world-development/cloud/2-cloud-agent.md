---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

技術的負債に苦労していない組織はほとんどありません。未解決のセキュリティ問題、更新が必要なレガシーコード、時間がないためバックログに残った機能要求などがあります。GitHub Copilot cloud agent は、コード更新や機能追加などのタスクを自律的に実行できます。作業を完了すると、人間の開発者がレビューできる draft PR を作成します。これにより定型作業を任せ、開発プロセスを加速し、開発者は大きな課題に集中できます。

Copilot cloud agentで次の内容を確認します。

- コード生成用の環境をカスタマイズする。
- 操作を安全に実行する。
- Issue のスコープを明確にする重要性。
- Issue を Copilot に割り当てる。

## シナリオ

Tailspin Toys には技術的負債があります。最初のサイトを作成した委託開発者はドキュメントを不十分な状態のままにしました。まず、エクスポートされたすべての関数に TSDoc コメントを追加してもらいます。

また、デザインチームはゲームの発見性を改善したいと考えています。各ゲームの詳細ページに、同じカテゴリーのほかのゲームを表示してブラウジングを続けられるようにします。完成度の高い実装ではなく、UX の受け入れテストに使えるものが必要です。

これらは、Copilot cloud agent に割り当てるのに適したタスクです。cloud agent が非同期で作業し、開発者はほかの作業をしてから Copilot の成果をレビューできます。

## GitHub Copilot cloud agent の概要

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者と同じようにバックグラウンドでタスクを実行できます。[GitHub Issue を Copilot に割り当てる](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)など、複数の方法があります。割り当てると、Copilot は進捗を追跡する draft pull request を作成し、環境をセットアップして作業を開始します。作業中や完了後にセッションを確認し、提案された解決策の準備ができると pull request で通知されます。

## スコープを明確にする指示の重要性

GitHub Copilot に魔法の機能はありません。簡単に見える操作でも、詳細を調べると複雑になるため、[Copilot cloud agent のタスク スコープを慎重に設定][cloud-agent-best-practices]してください。AI ペアプログラマーとして段階的に作業し、学習し、実験し、調整します。生成 AI を追加してもソフトウェア開発の基本は変わりません。

## リポジトリのカスタム指示

前の演習ではカスタム指示が Copilot に与える影響を確認しました。カスタム指示を使用しなかった場合でも、cloud agent に作業を割り当てる前にリポジトリの指示ファイルを読んでおくとよいでしょう。

GitHub Web UIまたは Codespace で、次のファイルを開きます。

- `.github/copilot-instructions.md`: **Code standards**セクション、特に TypeScript の規約と TSDoc コメントの要件を確認します。
- `.github/instructions/unit-tests.instructions.md`: `applyTo`フロントマターが`**/*.test.ts`ファイルを対象にしていることを確認します。

次のセクションで`Code lacks documentation` Issue を cloud agent に割り当てるとき、TSDoc コメント、TypeScript の規約、コメントヘッダーが pull request に含まれるか確認してください。

## Copilot cloud agent の開発環境を設定する

コードを作成するには、環境によっては特定のセットアップ スクリプトが必要です。Copilot にタスクを割り当てる場合も同様です。

cloud agent は作業環境に [GitHub Actions][github-actions]を使用します。[特別なセットアップ ワークフロー][setup-workflow]を作成し、`.github/workflows/copilot-setup-steps.yml`に構成すると、作業前にセットアップできます。これにより、必要な開発ツールと依存関係を利用できます。このラボでは、Node.js、プロジェクト依存関係、エンドツーエンド テスト用ブラウザー、移行とシード済みの SQLite データベースを利用できるよう事前設定されています。

```yaml
name: "Copilot Setup Steps"

# リポジトリの "Actions" タブからセットアップ手順をテストできるようにします
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 手順に必要な最小限の権限を設定します。Copilotには個別のトークンが付与されます。
    permissions:
      # セットアップ手順の一部としてリポジトリをクローンする場合 (依存関係のインストールなど) は `contents: read` 権限が必要です。この手順でクローンしない場合、Copilotが完了後に自動的にクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / app のセットアップ - Node.js (現在のアプリは Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ローカル SQLite データベースを移行してシードします。
      - name: Set up the database
        run: npm run db:setup
```

ワークフローの主な点は次のとおりです。

- `copilot-setup-steps`という単一ジョブが、Copilot が pull request の作業を開始する前に GitHub Actionsで実行されます。
- `workflow_dispatch`トリガーにより、**Actions**タブからワークフローを手動実行してテストできます。

## ドキュメントを追加する

ドキュメントの重要性は理解されていますが、多くのプロジェクトでは情報が古いか不足しています。これは、開発効率を低下させ、コードベースの保守や開発者の参加を難しくする技術的負債です。Copilot はドキュメント生成に優れているため、Copilot cloud agent に割り当てる適切な Issue です。

1. 新しいブラウザー タブで github.com のリポジトリに移動します。
2. **Issues**タブを選択します。
3. **New issue**を選択して新しい Issue ダイアログを開きます。
4. **Blank issue**を選択します。
5. **Title**に`Code lacks documentation`を設定します。
6. **Description**に次のテキストを設定します。

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. **Create**を選択します。
8.右側の **Assign to Copilot**を選択します。

  ![IssueにCopilotを割り当てる](../../../_images/shared-assign-copilot.png)

9. **Assign**を選択します。

  ![Copilotの割り当て詳細](../../../_images/ex4-assign-copilot-details.png)

10. **Pull Requests**タブを選択します。
11. `[WIP]: Code lacks documentation`のようなタイトルの新しい pull request を開きます。すぐに表示されない場合は、しばらく待ってから更新します。
12.数分後、Copilot が todo リストを作成していることを確認できます。

> [!NOTE]
> todo リストは数分後に表示される場合があります。Copilot は環境をセットアップし、プロジェクトを分析し、問題への最適な方法を決定します。

13. リストと実行予定のタスクを確認します。
14. pull request のタイムラインを下にスクロールし、Copilot が作業を開始したことを示す更新を確認します。
15. **View session**を選択します。

  ![Copilotセッションビュー](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 更新された状態を確認するには、ブラウザーを更新する必要がある場合があります。

16.ライブ セッションをスクロールし、Copilot がコードを調査し、計画を考え、コードを作成する様子を確認します。

## ゲーム詳細ページに関連ゲーム セクションを追加する

2つ目のタスクとして、デザインチーム向けの関連ゲーム セクションを Copilot cloud agent に割り当てます。

1. github.comでリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue**を選択します。
4. **Blank issue**を選択します。
5. タイトルを`Show related games on the game details page`に設定します。
6. 説明に次の内容を設定します。

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. **Create**を選択します。
8. **Assign to Copilot**を選択します。

  ![IssueにCopilotを割り当てる](../../../_images/shared-assign-copilot.png)

9. **Assign**を選択します。

Issue の最初のコメントに Copilot が作業中であることを示す👀が表示されるはずです。

## まとめと次のステップ

このレッスンでは、[GitHub Copilot cloud agent][copilot-agents]の概要、Issue の割り当て、非同期での作業、pull request のレビューを確認しました。

次は、[カスタム エージェント][next-lesson]を作成して使用します。

## リソース

- [Copilot cloud agent の概要][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent セットアップ ワークフローのベストプラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタム エージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
