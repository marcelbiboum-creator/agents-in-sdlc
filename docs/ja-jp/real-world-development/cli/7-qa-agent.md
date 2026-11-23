---
title: "レッスン 7 - QA エージェントの作成と使用"
description: "Issue の要件、quality-checks スキル、Playwright MCP を組み合わせる QA カスタム エージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

`quality-checks` スキルで自動チェックを実行し、Playwright MCP を使ってブラウザー上のフィルター体験を確認しました。次に、明確に定義された QA プロセスを持つカスタム エージェントにこれらの機能をまとめます。

このレッスンでは、次の内容を学習します。

- カスタム エージェントが指示、スキル、MCP ツールをどのように組み合わせるかを理解する。
- 再利用可能な品質保証プロファイルを作成して確認する。
- QA エージェントを選択し、フィルター Issue と照合して調査結果をレビューする。

## シナリオ

Tailspin Toys は、pull request (PR) を作成する前に、要件、コード品質、自動チェック、テスト カバレッジ、ブラウザーの動作を一貫してレビューしたいと考えています。カスタム エージェントは、その QA プロセスを調整し、再利用可能なレポートを提供できます。

## カスタム エージェントとは

カスタム エージェントは、Markdown プロファイルで定義される Copilot の専門バージョンです。目的、指示、利用可能なツールを記述します。このワークショップでは、QA の役割を `.github/agents/qa.agent.md` に定義し、Copilot CLI で選択します。

使用したカスタマイズには、それぞれ異なる役割があります。リポジトリの指示はチームの標準を示します。`quality-checks` スキルは繰り返し実行できるチェックをまとめます。Playwright MCP はブラウザー ツールを提供します。QA プロファイルは、要件を評価して調査結果を報告するためにこれらを使用する方法を Copilot に指示します。既存機能を置き換えたり、別の会話を必要としたりしません。

## QA プロファイルを作成する

フィーチャー PR を作成する前に、再利用可能な QA プロファイルを作成します。プロファイルには、QA が実行するチェックと守るべき境界を定義します。

1. Codespace に戻り、フィルター会話が Interactive モードであることを確認します。
2. デフォルト エージェントに、新しいカスタム エージェントの作成を依頼します。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

新しいエージェントを使用する前に、意図した QA ワークフローと境界が Copilot に反映されていることを確認します。これにより、不完全または範囲が広すぎるエージェントが検証だけを目的としているのに機能を変更することを防げます。

1. `/diff` を入力し、`.github/agents/qa.agent.md` を開きます。
2. フロントマターを確認します。`description` は必須ですが、`name` は任意です。含めるとエージェントの表示名が明確になります。
3. プロファイルの指示を読み、QA が要件を起点にし、リポジトリの指示に従い、`quality-checks` スキルを実行し、Playwright MCP を使用することを確認します。
4. QA が証拠付きでレポートし、実装コード変更前に確認し、コミットや pull request 作成を行わないことを確認します。
5. 生成されたプロファイルに責任や境界が不足している場合は、続行前にデフォルト エージェントに修正を依頼します。

## Issue に対して QA を実行する

プロジェクト エージェントは会話開始時に読み込まれます。プロファイル作成後に同じフィルター会話を再開し、QA を選択して Issue と計画の決定事項を利用できるようにします。

1. 次のプロンプトでエージェントを有効にします。

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> エージェントを作成したばかりの場合、利用可能なエージェントの一覧に表示されないことがあります。実際には利用可能です。上記のコマンドで有効化できます。

2. 次のプロンプトで QA エージェントにフィルター機能のレビューを依頼します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA エージェントの作業を確認します。
4. 作業完了後に提示されたレポートを確認します。

## まとめと次のステップ

再利用可能な専門エージェントをワークフローに追加し、その作業をレビューしました。このレッスンでは、次の内容を学習しました。

- カスタム エージェントが指示、スキル、MCP ツールをどのように組み合わせるかを理解した。
- 再利用可能な品質保証プロファイルを作成して確認した。
- QA エージェントを選択し、フィルター Issue と照合して調査結果をレビューした。

実装、スキル更新、QA プロファイル、テスト、検証レポートがレビュー可能な状態になりました。次は、[機能 PR にまとめて Agent Merge を使用][next-lesson]します。

## リソース

- [Copilot CLI 用カスタム エージェントを作成する][create-agents]
- [カスタム エージェントの構成][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
