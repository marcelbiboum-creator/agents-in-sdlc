---
title: "実践的な開発"
slug: ja-jp/real-world-development
authors:
  - geektrainer
lastUpdated: 2026-09-16
---

現実的なシナリオ、完成度の高いアプリケーション、共有されたバックログを使って、ソフトウェア開発ライフサイクル全体で GitHub Copilot を活用します。変更の計画、コードの作成、動作のテスト、pull request のレビュー、エージェントによる作業管理を反復的に行います。

## シナリオ

あなたは架空のボードゲームクラウドファンディング企業 Tailspin Toys の新しい開発者です。チームのバックログは GitHub issue として登録され、取り組む準備ができています。フィルターやページネーションなどの機能追加に加え、アクセシビリティやコーディング標準などの品質改善も含まれています。

## 環境を選ぶ

GitHub Copilot は、作業場所を問わず利用できます。自分がどの環境で開発したいかに合ったものを選択してください。各ワークショップは独自のセットアップから始まり、共通の Tailspin Toys シナリオを使用します。

### [GitHub Copilot CLI][cli]

ターミナルでエージェントを操作します。Plan モードと Autopilot モード、カスタム指示、スキル、カスタムエージェント、Playwright MCP、Agent Merge、実用的なスラッシュコマンドを使用します。

### [GitHub Copilot app][app]

デスクトップ アプリで並行してエージェント セッションを実行し、セッション モードを切り替え、キャンバスで共同作業を行い、GitHub issue と pull request を管理します。

### [GitHub Copilot cloud agent][cloud]

GitHub issue を非同期エージェントに割り当て、作業をガイドし、進捗を監視し、エージェントが作成した pull request をレビューします。

### [Visual Studio Code][vscode]

Visual Studio Code と GitHub Codespaces で GitHub Copilot を使用します。Copilot Chat のエージェント モード、MCP server、カスタム エージェントを使って、エディターを離れずに作業します。

[cli]: cli/
[app]: app/
[cloud]: cloud/
[vscode]: vscode/
