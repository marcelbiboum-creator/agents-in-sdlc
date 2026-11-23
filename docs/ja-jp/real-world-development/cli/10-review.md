---
title: "レッスン 10 - 振り返りと次のステップ"
description: "Copilot CLI のワークフロー、2つの pull request、再利用可能なカスタマイズ、追加リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

GitHub Copilot CLI を使って、Tailspin Toys の一連のワークフローを進めました。実施した内容は次のとおりです。

- Codespace を準備し、Copilot CLI をインストールして、プロジェクトを確認し、用意されたフィルター Issue を見つけた。
- 星評価を追加し、転送されたブラウザーで結果をレビューし、最初の pull request (PR) を手動でマージした。
- フィルター Issue を起点にし、Plan モードでアプローチを定義し、Autopilot モードで構築し、Interactive モードでレビューした。
- カスタム指示でエージェントをガイドし、既存の `quality-checks` スキルをカスタマイズして、単体テスト、lint、型チェックを実行した。
- Playwright Model Context Protocol (MCP) server を追加し、実際のブラウザーでフィルター機能を確認した。
- 要件、カバレッジ、スキルの結果、ブラウザーの証拠を評価する品質保証 (QA) カスタム エージェントを作成して選択した。
- フィルター機能の変更全体をレビューし、フィルター PR に Agent Merge を承認した。
- コンテキスト、モデル、共有、任意のクラウド委任に関するスラッシュコマンドを確認した。

## 完成したもの

ワークショップには2つの PR マイルストーンがあり、それぞれ更新済みの `main` から作成した専用ブランチを使用します。

1. **星評価:** ゲームカードに既存の `starRating` と明示的な未評価状態を表示します。
2. **フィルターと品質ワークフロー:** フィルターを実装し、指示を更新してフィルター機能に適用し、`quality-checks` レポートをカスタマイズして、QA プロファイルと関連するテストを追加します。

フィルター機能の計画から PR の作成まで、同じ会話とブランチを使用しました。ワークショップを簡潔に進めるため、この作業を1つの PR にまとめました。

## 検証方法の違い

自動テスト、自分によるブラウザー確認、MCP を介した Copilot によるブラウザー調査という複数の方法でコードを確認しました。`quality-checks` スキルは単体テスト、lint、型チェックを実行し、新しい形式で結果を報告しました。PR を作成する前に、QA は要件とテストカバレッジのレビューとこれらの結果を組み合わせました。

追加するテストは実際の不足を補うものにします。新しいテストを必要としない QA 実行でも正しい場合があります。ツールの不足、スキップされたチェック、失敗は成功ではなく、明示すべき問題です。マージを承認する前にコードと証拠をレビューし、変更後は影響を受ける証拠を更新してください。

## ベストプラクティス

Copilot に与えるコンテキストとツールが、その作業を左右します。このワークショップでは、指示を更新し、スキルをカスタマイズして、QA プロファイルを作成し、MCP server を設定しました。これらのカスタマイズを会話間で再利用し、チームのニーズに合わせて調整してください。指示は標準を定め、スキルは繰り返しのタスクを説明し、カスタム エージェントは専門的な役割を定義し、MCP server は外部ツールを接続します。エージェントの要約だけでなく、実際の変更とツールの結果をレビューしてください。

タスクに合わせて**モードとモデル**を選びます。構築前にアプローチを検討するには **Plan**、対象を絞った変更で作業に関与し続けるには **Interactive**、範囲が明確で隔離されたタスクには **Autopilot** を使用します。定型的な編集には高速なモデルを選び、複雑な作業には推論能力が高いモデルを選びます。

コンテキストは基盤と同じくらい重要です。何を、なぜ、どのように構築するかを明確に説明すると、出力は大きく変わります。

## 確認できる機能

コア ワークフローを完了しました。確認に値する CLI 機能がいくつかあります。

- `/review` でコードレビュー エージェントに変更を分析させます。
- `/rubber-duck` で問題について話し合い、別の視点を得ます。
- `/fleet` で独立したサブタスクを並列に調整します。
- `/worktree` で別のタスクを隔離した Git worktree を作成します。
- `/delegate`でタスクを Copilot cloud agent に送ります。

## 次のステップ

ツールの使い方を改善する最良の方法は、使い続けることです。プロダクトコード、趣味のコード、何年も構想しているがまだ作れていない小さなアプリに活用してください。チームと学びを共有し、チームの経験から学びましょう。そしてドキュメントも確認してください。

ターミナルから Tailspin Toys を拡張する場合は、任意の [Foundry Backer Concierge シリーズ][foundry]に進んでください。ほかの環境と比較する場合は、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、[Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI の概要][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI のカスタマイズ][customize-cli]
- [Copilot CLI で pull request を管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
