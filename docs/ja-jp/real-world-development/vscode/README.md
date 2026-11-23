---
slug: ja-jp/real-world-development/vscode
title: "Visual Studio Code"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

VS Code の **[GitHub Copilot Chat](https://code.visualstudio.com/docs/copilot/chat/copilot-chat)**を使うと、普段のコード エディターで GitHub Copilot を利用できます。Visual Studio Code (および GitHub Codespaces) で、Copilot Chat のエージェント モードを操作し、MCP を通じて外部ツールを接続し、カスタム エージェントを活用します。IDE を離れずに進められるため、Copilot はファイル、ターミナル、問題をまとめて把握できます。

まずカスタム指示を追加し、Copilot が指示に従う様子を確認します。次にエージェント モードで、UI、データ層、テストにまたがるフィルター機能を構築します。その後、Playwright MCP serverを接続し、pull requestを作成する前に Copilot にブラウザーを操作させて機能をテストします。最後に、アクセシビリティ作業用のカスタム エージェントを確認して使用し、Copilot の変更を監視して方向付けしながら反復改善します。

## 演習

| 演習 | トピック | 説明 |
|----------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成する |
| [1. カスタム指示][ex1] | コンテキスト | VS Codeでカスタム指示を追加して検証する |
| [2. エージェント モード][ex2] | コード生成 | エージェント モードでフィルター機能を構築する |
| [3. Playwright MCP によるテスト][ex3] | 外部ツール | Playwright MCP serverを使ってブラウザーで機能をテストする |
| [4. カスタム エージェント][ex4] | 専門エージェント | カスタム エージェントを確認して使用する |
| [5. エージェントの管理][ex5] | 監視 | エージェント セッションを監視して方向付けする |
| [6. 反復改善][ex6] | レビュー | Copilot の作業をローカルでレビューし、次のステップを選ぶ |
| [省略可能: Foundry を組み込む][foundry-toolkit] | AI エージェント | VS Code と Foundry Toolkit を使う3モジュールで、モデルを準備し、エージェントをデプロイしてサイトに接続する |

## 前提条件

このワークショップに参加する前に、次のものを用意してください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、Enterprise** のいずれかのプランがある GitHub アカウント
- [ ] GitHub Codespaces へのアクセス

> [!TIP]
> 有料プランを利用していない場合、認証済みの学生は [GitHub Education][callout-student-plan-education]を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使用するエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれます。

[callout-student-plan-education]: https://github.com/education/students

## はじめる

**[演習 0: 前提条件から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-agent-mode/
[ex3]: 3-mcp/
[ex4]: 4-custom-agents/
[ex5]: 5-managing-agents/
[ex6]: 6-iterating/
[foundry-toolkit]: 7-foundry-toolkit/
