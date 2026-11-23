---
slug: ja-jp/real-world-development/app
title: "GitHub Copilot app"
description: "Tailspin Toys の変更を構築、検証、提供しながら、Copilot app のモード、カスタマイズ、MCP ツール、pull request 自動化を学びます。"
authors:
  - geektrainer
lastUpdated: 2026-09-17
---

[**GitHub Copilot app**](https://docs.github.com/copilot/concepts/agents/github-copilot-app)は、Copilot CLI を基盤とするデスクトップ アプリケーションで、エージェント主導の開発を単一のワークスペースで実現します。並列エージェント セッション、切り替え可能なセッション モード、共有キャンバス、GitHub Issue と pull request のネイティブ管理機能を備えています。リベース、レビュー フィードバック、継続的インテグレーション (CI) 修正、マージまで pull request をガイドする **Agent Merge**も利用できます。

このワークショップでは、Tailspin Toys の一連のワークフローに取り組みます。

1. プロジェクトを準備し、appをインストールしてリポジトリを接続し、ワークスペースと用意されたバックログを確認します。
2. 対象を絞った星評価の変更を行い、ブラウザーでレビューして、最初の pull request (PR) を手動でマージします。
3. フィルター Issue を起点にし、**Plan**モードでアプローチを定義し、**Autopilot**モードで構築し、**Interactive**モードでレビューします。
4. リポジトリの指示を更新し、フィルター作業に適用します。
5. 既存の`quality-checks`スキルをカスタマイズし、プロジェクトのチェックに使用します。
6. Playwright Model Context Protocol (MCP) serverを追加し、ブラウザーでフィルター機能を確認します。
7. 品質保証 (QA) カスタム エージェントを作成し、要件、カバレッジ、検証証拠をレビューします。
8. フィルター機能の変更全体をレビューし、2つ目の PR に Agent Merge を使用します。
9. 既存の Database Explorer キャンバスを使い、リポジトリに保存するトリアージ キャンバスを作成してテストします。

ワークショップの焦点を絞るため、2つの PR を作成します。星評価、続いてフィルター機能と指示、スキル、QA プロファイル、テストの更新です。フィルター機能と品質ワークフローでは1つのセッション、worktree、ブランチを共有し、各ツールを確認しながら作業を積み重ねます。

## レッスン

| レッスン | トピック | 説明 |
|--------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | Node.js をインストールし、Tailspin Toys プロジェクトの自分用コピーを作成する |
| [1. Copilot app のインストール][ex1] | セットアップ | appをインストールしてプロジェクトを接続し、ワークスペースを確認する |
| [2. 星評価の追加で小さな成果を得る][ex2] | 最初の変更 | 既存の評価と null の場合の表示を追加し、最初の PR をマージする |
| [3. エージェント モード: Plan と Autopilot][ex3] | エージェント モード | Issue から機能を計画し、Autopilot で構築し、Interactive モードでレビューする |
| [4. カスタム指示で Copilot をガイドする][ex4] | コンテキスト | 指示を確認して更新し、フィルター機能に適用する |
| [5. quality-checks スキルのカスタマイズと使用][ex5] | 繰り返し実行できるチェック | 既存のスキルを確認し、レポート形式を変更して実行する |
| [6. Playwright MCP による機能の検証][ex6] | ブラウザーでの観察 | Customize から MCP を設定し、フィルターの動作を確認する |
| [7. QA エージェントの作成と使用][ex7] | 要件とカバレッジ | 専門プロファイルを作成して選択し、最終検証の証拠を収集する |
| [8. 機能 PR の作成とマージ][ex8] | レビューとマージ | 完全な変更をレビューし、PR を作成して Agent Merge を使用する |
| [9. キャンバスの確認と作成][ex9] | コラボレーション | Database Explorer を使い、リポジトリに保存するトリアージ キャンバスを作成してテストする |
| [10. 振り返りと次のステップ][ex10] | まとめ | ワークフロー、成果物、追加リソースを振り返る |

## 前提条件

このワークショップに参加する前に、次のものを用意してください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、Enterprise** のいずれかのプランがある GitHub アカウント
- [ ] **macOS、Linux、Windows**のいずれかを実行するコンピューター
- [ ] コンピューターに[インストールされた Git][install-git]

> [!TIP]
> 有料プランを利用していない場合、認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使用するエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれます。

> [!NOTE]
> Copilot app は Codespaceではなく自分のコンピューターで実行するため、[レッスン 0][ex0]で appをインストールする前に Node.js をインストールし、プロジェクトの自分用コピーを作成します。

> [!NOTE]
> Copilot Business または Copilot Enterprise を使用している場合、appを使用するには管理者が **Copilot CLI** ポリシーを有効にする必要があります。

## はじめる

[**レッスン 0「前提条件」から始める →**][ex0]

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-app/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-canvases/
[ex10]: 10-review/
[install-git]: https://github.com/git-guides/install-git
[callout-student-plan-education]: https://github.com/education/students
