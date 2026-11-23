---
title: "レッスン 4 - カスタム指示で Copilot をガイドする"
description: "リポジトリの指示を確認し、ドキュメント標準を追加し、フィルターコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使ううえでコンテキストは重要です。タスクを特定の方法で実行する必要がある場合は、そのガイドを Copilot が利用できるようにします。[指示ファイル][instruction-files]は、必要なコードだけでなく、コードをどのように構造化するかを示します。フィルター機能を構築したところで、Copilot が使用した指示を確認し、ドキュメント標準を追加し、コードに適用します。

このレッスンでは、次の内容を学習します。

- リポジトリの指示とパス スコープの指示ファイルがエージェントに届く仕組みを確認する。
- コーディング標準を守るよう指示ファイルを更新する。
- 指示ファイルがコードに与える影響を確認する。

## シナリオ

優れた開発チームと同様に、Tailspin Toys には開発プラクティスに関するガイドラインと要件があります。

- コメントはコードを言い換えず、意図や自明でない判断を説明します。
- `db/` と `src/lib/` のエクスポートされた関数は、ある場合は依存性注入可能な `db` 引数も含め、目的、パラメーター、戻り値を TSDoc/JSDoc で文書化します。
- 再利用可能な Astro コンポーネントは `Props` の契約を文書化し、関連コードが変更されたらコメントも更新します。
- 既存のフォーマットと lint のガイドを維持します。

指示ファイルを使うことで、Copilot がこのプラクティスに沿った情報を利用できるようになります。

## 指示ファイル

カスタム指示を使うと、Copilot にコンテキストと好みを与え、コーディング スタイルと要件を理解させることができます。関連する提案とコード スニペットを得やすくなり、コーディング規約、ライブラリ、コメントの種類を指定できます。リポジトリ全体または特定のタスクに対して指示を作成できます。

指示ファイルには2種類あります。

- `.github/copilot-instructions.md`: リポジトリへの**すべての**要求に送られる単一の指示ファイル。ほとんどの要求に関係するプロジェクトレベルの情報を記述します。
- `.github/instructions/*.instructions.md`: 特定の言語、ファイル種別、タスク向けのガイドラインを提供します。

> [!NOTE]
> その他の指示形式とサポート状況は環境によって異なります。特定の形式に依存する前に、[カスタム指示のサポート リファレンス][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム指示ファイルを確認する

スターター プロジェクトには、すでに一式の指示ファイルが含まれています。変更を加える前に内容を確認し、影響を確認しましょう。

1. Codespace に戻ります。
2. Codespaces エディター (ターミナルではない) で `.github/copilot-instructions.md` を開きます。
3. プロジェクトの概要とコーディング ガイダンスを確認します。このリポジトリで Copilot と対話するとき、これらの指示が適用されます。
4. `.github/instructions` フォルダーを開き、ファイルを確認します。Astro ファイル、Drizzle データ層、テストなどの指示があります。
5. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドは、指示を適用するファイルを決める glob を設定します。
6. `.github/instructions/drizzle.instructions.md` を開き、ほかの指示ファイルや既存プロジェクト ファイルへのリンクを確認します。大きな指示セットを再利用可能な小さなファイルに分割し、従うべき例を示せます。

## チームのガイドに合わせて指示ファイルを更新する

既存のファイルは有効な出発点ですが、不足があります。コアの `copilot-instructions.md` を変更し、新しく生成する TypeScript に TSDoc コメントを追加させます。

1. `.github/copilot-instructions.md` で、35行付近にある **Code formatting guidance** セクションを探します。
2. 次の内容を最後の箇条書きとして追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

ファイルは自動保存されます。

## 更新したガイドを使用する

Copilot CLI は会話開始時にリポジトリの指示を読み込みます。更新した指示を保存したら、フィルター会話を終了して再開し、フィルターのコンテキストを失わずに新しいガイドを読み込ませます。

1. フィルター会話が開いている場合は、`/exit` を入力して終了します。Copilot CLI は会話を自動保存します。
2. `game-filters-cli` ブランチのリポジトリ ルートから、保存済み会話を再開します。

   ```bash
   copilot --resume
   ```

   プロンプトが表示されたらフィルター会話を選択し、`game-filters-cli` ブランチがチェックアウトされていることを確認します。
3. Copilot に更新したガイドの適用を依頼します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力し、変更された TypeScript ファイルを確認します。新しく生成された TSDoc コメントがコードを正確に説明していることを確認します。

## まとめと次のステップ

Copilot CLI が指示ファイルからコンテキストを取得する仕組みを確認し、フィルター機能に新しい標準を適用しました。具体的には、次の作業を行いました。

- リポジトリの指示とパス スコープの指示ファイルがエージェントに届く仕組みを確認した。
- コーディング標準を守るよう指示ファイルを更新した。
- 指示ファイルがコードに与える影響を確認した。

次は、[再利用可能な quality-checks スキルをカスタマイズして実行][next-lesson]し、lint とテストが一貫して実行されるようにします。

## リソース

- [Copilot CLI にカスタム指示を追加する][instruction-files]
- [カスタム指示のサポート][custom-instructions-support]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Awesome Copilot — 指示ファイルのコレクション][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
