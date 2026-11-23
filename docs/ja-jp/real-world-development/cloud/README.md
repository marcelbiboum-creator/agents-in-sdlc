---
slug: ja-jp/real-world-development/cloud
title: "GitHub Copilot cloud agent"
description: "Copilot cloud agent を使って Issue の割り当て、作業の監視、カスタム エージェントの利用、pull request の反復レビューを学びます。"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent) を使うと、GitHub Copilot はクラウドで非同期に作業できます。GitHub 上で作業を割り当てると、cloud agent がバックグラウンドでリポジトリを調査し、変更を加え、pull request を作成します。ユーザーはほかの作業を続けられます。

演習では、cloud agent が従うカスタム指示を追加し、GitHub Issue を割り当てて実装させます。カスタム エージェントでアプローチを調整し、エージェント ダッシュボードでセッションを監視して方向付けし、pull request をレビューして結果を反復改善します。

## 演習

| 演習 | トピック | 説明 |
|----------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと codespace を作成する |
| [1. カスタム指示][ex1] | コンテキスト | cloud agent が従うカスタム指示を追加する |
| [2. Cloud agent][ex2] | 非同期エージェント | Issue を Copilot cloud agent に割り当てる |
| [3. カスタム エージェント][ex3] | 専門エージェント | カスタム エージェントを確認して使用する |
| [4. エージェントの管理][ex4] | 監視 | エージェント セッションを監視して方向付けする |
| [5. 反復改善][ex5] | レビュー | PR を確認し、Copilot の作業を反復改善して次のステップを選ぶ |

## 前提条件

このワークショップに参加する前に、次を準備してください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、Enterprise** のいずれかのプランがある GitHub アカウント
- [ ] アカウントまたは organization で Copilot cloud agent が有効になっている

> [!TIP]
> 有料プランがありませんか。認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。

> [!NOTE]
> Cloud agent は **Copilot Student、Pro、Pro+、Business、Enterprise** で利用できます。Copilot Free を除きます。Copilot Business または Enterprise の場合、管理者が organization で有効化する必要があります。

> [!NOTE]
> このハーネスでは MCP は扱いません。CopilotでMCP serverを使う方法は、[CLI ハーネス](../cli/)または[VS Code ハーネス](../vscode/)を参照してください。

## はじめる

**[演習 0: 前提条件から始める →][ex0]**

[callout-student-plan-education]: https://github.com/education/students
[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
