---
title: "レッスン 5 - quality-checks スキルのカスタマイズと使用"
description: "既存の quality-checks スキルを確認し、レポート形式をカスタマイズして、フィルター機能の検証に使用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

コードを書くことだけが仕事ではありません。手動で動作を検証し、指示ファイルで標準への準拠を確認できました。では、テストや lint、継続的インテグレーション (CI) のほかの要素はどうでしょう。

この種のタスクには、**エージェント スキル**が最適です。スキルは、Copilot が操作の正しい実行方法を理解するのに役立ちます。

このレッスンでは、次の内容を学習します。

- 既存の `quality-checks` スキルを確認する。
- 結果の形式をカスタマイズする。
- スキルをリロードして実行する。

## シナリオ

Tailspin Toys では、`quality-checks` スキルを使って単体テスト、lint、型チェックを実行します。チームは結果を読みやすくするためレポートを改善したいと考えています。

## 指示、スクリプト、リソース

エージェント スキルは、再利用可能なタスク指示、実行可能スクリプト、補助リソースをまとめます。基本的には、スキル名のフォルダーに `SKILL.md` という Markdown ファイルがあります。この Markdown のフロントマターにはスキルの名前と説明があり、概要と呼び出すべき状況を示します。スキルが使用するスクリプトやほかのリソース用のサブフォルダーを含めることもできます。

> [!NOTE]
> スキルにサブフォルダーやファイルは必須ではありません。Tailspin Toys の `quality-checks` スキルには、プロジェクトの既存コマンドを使うため `SKILL.md` だけが含まれています。

スキルは、チームで共有し再利用するリポジトリ資産としてプロジェクトの `.github/skills` フォルダーに配置できます。ユーザー スキル フォルダーの `~/.copilot/skills` に配置することもできます。

## スキルを確認する

Tailspin Toys チームが作成した、単体テスト、lint、型チェックを実行する `quality-checks` スキルを確認します。

1. Codespace に戻り、Codespaces エディターで `.github/skills/quality-checks/SKILL.md` を開きます。
2. 先頭の `name` と `description` を確認します。description は、Copilot がスキルをいつ呼び出すか判断するのに役立ちます。
3. 指示を読み、テストと lint の実行方法を確認します。
4. スキルに **Results output formatting** セクションがまだないことを確認します。

## 変更前にスキルを実行する

スキルは Copilot CLI から直接、または自然言語で呼び出せます。Copilot にスキルの3つのチェックを実行させます。

1. Interactive モードのフィルター会話に戻ります。
2. 次のプロンプトを使います。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後のレポートを確認します。

## レポートをカスタマイズする

実行された内容、成功したか、ツールが実際に報告した内容を示す、読みやすいレポートが必要です。スキルを更新してレポートを作成しましょう。

1. `.github/skills/quality-checks/SKILL.md` に戻ります。
2. ファイルの末尾に次のセクションを追加します。

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. ファイルは自動保存されます。

## 更新したスキルを実行する

変更を加えたので、実際に動作を確認します。Copilot CLI は会話を再起動せずに、編集されたスキルをリロードできます。

1. 次を入力します。

   ```plaintext
   /skills reload
   ```

2. 先ほどと同じプロンプトを使います。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後のレポートを確認し、最初のレポートと比較します。

## まとめと次のステップ

既存のエージェント スキルをカスタマイズして使用しました。このレッスンでは、次の作業を行いました。

- 単体テスト、lint、型チェックを実行する `quality-checks` スキルを確認した。
- 結果の形式をカスタマイズした。
- スキルをリロードして実行した。

この変更はフィルター機能とともにフィーチャー PR に含められます。次は、[Playwright MCP server経由][next-lesson]で Copilot がサイトと直接対話できるようにします。

## スキルのほかの例

次のコミュニティ例は参考資料であり、追加タスクではありません。

- [エージェント スキル仕様][skill-spec]
- [Contribution workflow: `make-repo-contribution`][contribution-example]
- [要件ドキュメント: `prd`][prd-example]
- [図とバンドル済みエクスポート スクリプト: `drawio`][drawio-example]
- [ブラウザー テスト: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
