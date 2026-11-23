---
title: "レッスン 8 - 機能 PR の作成とマージ"
description: "フィルター、指示、スキル更新、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

フィルター実装、指示の更新、スキルの更新、品質保証 (QA) プロファイル、テストは1つのブランチに保存されています。次にこれらをまとめてレビューし、pull request を作成します。星評価の pull request (PR) は手動でマージしました。今回は、**Agent Merge** に作業を任せます。

> [!NOTE]
> 通常は、フィルター機能、指示の更新、スキル更新、QA エージェントを複数の PR に分割します。このワークショップでは簡潔さを優先し、フィルターと品質ワークフロー全体を1つの会話とブランチにまとめ、この PR に含めています。

このレッスンでは、次の内容を学習します。

- Agent Merge と、マージライフサイクルの自動化方法を理解する。
- 完全なフィルター変更と検証証拠を確認する。
- フィルター PR を作成する。
- レビュー後にだけ Agent Merge を有効にし、PR がマージされたことを確認する。

## シナリオ

フィルター ワークフロー全体で、Copilot に計画、実装、検証を依頼しました。Tailspin Toys は、マージ承認を開発者が管理しながら、残りの PR 作業を自動化したいと考えています。

## Agent Merge の概要

**Agent Merge** は、pull request をマージするために必要な作業を自動化します。有効化すると、Copilot は失敗している継続的インテグレーション (CI) チェックの修正、レビュー コメントへの対応、必要に応じたリベースなど、PR をブロックしている要因を解決し、リポジトリで許可されていれば GitHub 自動マージを有効にします。

これまで、**Merge pull request** は学習者が選択していました。Agent Merge にその責任を任せられます。作業をレビューし、準備ができていると判断してから Agent Merge を有効にしてください。

## Agent Merge を使って PR を管理する

コードが作成されたので、まとめてレビューし、PR を作成し、残りのプロセスを Agent Merge に任せます。

1. Codespace に戻ります。
2. `/agent` を入力してエージェント ダイアログを開きます。
3. オプション一覧から **Default** を選択し、<kbd>Enter</kbd> を押します。
4. `/pr create` コマンドで新しい PR を作成します。
5. `/pr agentmerge` を使って Agent Merge を有効にします。
6. Copilot は PR の継続的インテグレーション プロセスを監視します。すべてが成功するとマージを実行します。
7. `"PR #14 was squash-merged successfully."` のような Copilot の成功メッセージが表示されることを確認します。

> [!IMPORTANT]
> Agent Merge は、必須承認、ブランチ保護、マージキュー、リポジトリ設定、不足する権限を回避しません。ブロックされた場合は、報告された理由を確認し、リポジトリで許可されている場合はレビュー済みマージを手動で完了してください。

## まとめと次のステップ

コードの生成、テストと検証、pull request の処理など、開発プロセスの一部を自動化しました。

- Agent Merge とマージライフサイクルの自動化方法を理解した。
- 完全なフィルター変更と検証証拠を確認した。
- フィルター PR を作成した。
- レビュー後に Agent Merge を有効にし、PR がマージされたことを確認した。

次は、コンテキスト、モデル、共有、任意のクラウド委任に関する [Copilot CLI のほかの便利なスラッシュコマンド][next-lesson]を確認します。

## リソース

- [Copilot CLI で pull request を管理する][manage-prs]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
