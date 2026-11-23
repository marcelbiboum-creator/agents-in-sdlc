---
title: "レッスン 9 - GitHub Copilot CLI のスラッシュコマンド"
description: "コンテキスト管理、モデル選択、セッション共有、任意のクラウド委任に使うスラッシュコマンドを確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

優れた CLI ツールと同様に、GitHub Copilot CLI には操作に使える多くのスラッシュコマンドがあります。高度な機能、内部情報、追加の構成オプションを提供します。すでに `/diff`、`/mcp`、`/skills`、`/agent`、`/pr` を使用しました。ここでは、ほかの便利なコマンドを確認します。

このレッスンでは、次の内容を学習します。

- `/context` と `/compact` を使って Copilot の会話コンテキスト管理を確認する。
- `/model` を使って利用可能なモデルを確認する。
- `/share` によるセッションのエクスポートまたは共有方法を理解する。
- 並列作業、worktree、cloud agent への委任に使う任意のコマンドを確認する。

## シナリオ

コアとなる CLI ワークフローを完了しました。次に、コンテキスト管理、モデル切り替え、セッション共有、必要に応じて [Copilot cloud agent][about-cloud-agent]へ委任するなど、追加機能を確認します。

## Copilot CLI のコンテキストを確認する

規模が大きい複雑なタスクでは、モデルの最大コンテキスト ウィンドウに達する場合があります。Copilot CLI は必要に応じて会話を自動圧縮し、スラッシュコマンドで確認または手動圧縮できます。

1. Codespace に戻り、まだ開いていない場合はリポジトリのルートから Copilot CLI を起動します。
2. 次を入力します。

   ```plaintext
   /context
   ```

3. モデル、現在のトークン使用量、システム指示、ツール、メッセージ、空き領域に分けたコンテキストを確認します。
4. 会話を圧縮します。

   ```plaintext
   /compact
   ```

5. 再び `/context` を入力し、結果を比較します。会話がすでに小さい場合は大きな変化がないことがあります。

> [!NOTE]
> コンテキスト ウィンドウが満杯になると、Copilot CLI は会話を自動圧縮します。タイミングを選びたい場合は `/compact` を使用します。無関係なタスクに切り替えて新しい会話から始める場合は `/clear` または `/new` を使用します。

## モデルを選ぶ

モデルごとに得意分野が異なり、開発者ごとに好みもあります。Copilot CLI では、利用可能なモデルを一覧表示し、使用するモデルを選択できます。

1. 次を入力します。

   ```plaintext
   /model
   ```

2. 利用可能なモデルと使用量情報を確認します。
3. 現在のモデルを維持するか、別のモデルを選択するか、<kbd>Esc</kbd> を押して一覧を閉じます。

## セッションを共有する

チームで協力し、学びを共有することで、AI ツールの活用を改善できます。`/share` コマンドは、セッションを Markdown または HTML ファイルにエクスポートし、共有可能なリンクを作成し、GitHub gist を公開できます。

1. `/help` を入力し、インストール済みバージョンの `/share` オプションを確認します。
2. セッションを共有する場合は、ローカルの Markdown エクスポートには `/share file` など、目的に合った保存先を選択します。
3. 誰かに送信したり公開したりする前に、エクスポート内容を確認します。セッション エクスポートにはプロンプト、応答、プロジェクトの詳細が含まれる場合があります。

リンクや gist の公開は任意です。チームが共有しない意図のリポジトリや会話の内容は公開しないでください。

## 任意: スケールアウトまたは委任

コア ワークショップは完了しました。Copilot CLI は規模の大きいタスク向けに追加コマンドを提供します。

- `/fleet` は、独立したサブタスクをサブエージェントに分配し、並列実行します。
- `/worktree` は、別タスク用に隔離された Git worktree を作成します。
- `/delegate` は、タスクを Copilot cloud agent に送ります。cloud agent は非同期で動作し、pull request を作成する場合があります。

これらのコマンドは任意です。追加の worktree またはリモート作業が発生するためです。試す前に、範囲が明確で新しいタスクを開始し、通常のワークフローで結果を確認してください。非同期エージェント作業を詳しく確認する場合は、[cloud agent ワークショップ][cloud-workshop]に進んでください。

## まとめと次のステップ

Copilot CLI のスラッシュコマンドを使うと、構成、セッション共有、内部動作の確認ができます。このレッスンでは、次の内容を学習しました。

- `/context` と `/compact` を使って Copilot の会話コンテキスト管理を確認した。
- `/model` を使って利用可能なモデルを確認した。
- `/share` によるセッションのエクスポートまたは共有方法を理解した。
- 並列作業、worktree、cloud agent への委任に使う任意のコマンドを確認した。

ほかにもスラッシュコマンドがあり、Copilot CLI で確認できることは多数あります。[学習内容を振り返り][next-lesson]、学習を続けるための次のステップを確認しましょう。

## リソース

- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI のコンテキスト管理][context-management]
- [Copilot cloud agent の概要][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
