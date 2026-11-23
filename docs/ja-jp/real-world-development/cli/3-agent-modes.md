---
title: "レッスン 3 - エージェント モード: Plan と Autopilot"
description: "Plan でアプローチに合意し、Autopilot で Issue からフィルター機能を構築し、Interactive モードで結果をレビューします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

小規模な機能をプロジェクトに追加しましたが、規模が大きい変更には、より堅牢なプロセスが必要です。GitHub Copilot CLI は組織の既存のワークフローに合わせて動作し、適切なものを適切な方法で構築できます。このレッスン以降では、Issue を使って新機能を生成し、コードが有効で動作が期待通りかを確認し、最終的にプロジェクトへマージするという、エージェント主導の一般的な開発プロセスをたどります。

> [!NOTE]
> 機能の処理を続ける間も、同じ会話とブランチを使用します。通常、作業するファイル種別ごとに異なるブランチや PR を使いますが、このワークショップでは、コア概念に集中できるようショートカットを使用します。

このレッスンでは、次の内容を学習します。

- GitHub Issue から新しい Copilot 会話を開始する。
- Plan モードで要件を定義する。
- Autopilot モードで新機能を実装する。
- コードをレビューする。
- 転送されたブラウザーで機能を手動検証する。

機能を進めるうえで、リポジトリの指示を更新し、既存の `quality-checks` スキルをカスタマイズし、MCP による検証を追加し、QA エージェントを作成し、機能 PR を作成します。

## シナリオ

Tailspin Toys のカタログは拡大しており、訪問者はカテゴリーとパブリッシャーでゲームを絞り込む必要があります。バックログ Issue に機能の概要はありますが、カテゴリーの組み合わせ方などの詳細は、コーディング前に合意が必要です。Plan モードで決定事項を整理し、Autopilot で範囲を限定した実装を承認します。

## 背景

開発フローに AI コーディング エージェントを導入しても、基本原則は変わりません。むしろ重要性は高まります。多くの開発者は次のような流れをたどります。

1. 対処すべき内容を記述した Issue を起点にする。
2. 構築内容の計画を作成する。
3. コードを構築してレビューする。
4. テストを実行してコードを検証する。
5. 新機能を手動で検証する。
6. pull request (PR) を作成する。
7. コードをレビューし、継続的インテグレーションのプロセスが成功したらマージする。

> [!NOTE]
> チームや組織によって、具体的な手順は異なる場合があります。しかし、多くは上記の流れのバリエーションです。

この標準的なアプローチを守ることで、AI が生成したコードが要件を満たし、手作業のコードと同じ検証プロセスを経ることを確認できます。

## 会話モード

**会話モード**は、エージェントの自律性を決めます。<kbd>Shift</kbd>+<kbd>Tab</kbd> を押してモードを切り替えます。

- **Interactive:** ユーザーとエージェントが協力します。エージェントは変更案を提示し、次の操作前に入力を待ちます。
- **Plan:** エージェントが先に計画を作成し、プロジェクト ファイルの編集は禁止されます。
- **Autopilot:** エージェントがコードを書き、テストを実行し、タスクが完了するまで反復します。

Plan モードで開始し、計画をレビューした後、Autopilot モードで実装します。

## Issue から開始する

フィルター作業を始める前に、Codespace に戻り、リポジトリとターミナルが準備できていることを確認します。

1. Codespace に戻ります。停止している場合は、続行前に再起動します。
2. 星評価の PR がマージ済みであることを確認します。
3. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
4. `main` を更新し、フィルター作業用のブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

6. <kbd>Tab</kbd> を2回押して **Issues** タブを開きます。
7. <kbd>A</kbd> を押してすべての Issue を表示します。
8. 矢印キーで、**Allow users to filter games by category and publisher** というタイトルの Issue を選択します。
9. <kbd>C</kbd> を押して Issue をプロンプトに追加し、**Session** タブに戻ります。

プロンプトが `#7` (または類似の番号) から始まることを確認します。`#` を使うと、GitHub の Issue または pull request (PR) をコンテキストに追加できます。

## フィルター機能を計画する

計画を作成すると、Copilot に引き継ぐ前に機能の実装方法やタスクの進め方を定義できます。複雑な作業では、計画に時間をかけることをお勧めします。Plan モードに切り替え、Copilot に計画を作成させます。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Plan モードに切り替えます。プロンプト下のモード表示が **Plan** になっていることを確認します。
2. 前の手順で追加した Issue 参照の後に、次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot は計画を作成します。まずプロジェクトを調査し、最適なアプローチを決定します。

3. フィルター機能の動作について Copilot が質問する場合があります。好みに基づいて回答します。正解は1つではありません。
4. 計画が完了したら、<kbd>Control</kbd>+<kbd>E</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) を押して計画を展開します。
5. 上下にスクロールして計画を確認します。
6. 決定事項と一致しない箇所を、Copilot に修正させます。

## Autopilot を承認する

計画を作成してレビューしたら、実装を始めます。Copilot に任せるために Autopilot を使用します。

Autopilot により、Copilot はタスクが完了したと判断するまで反復します。

1. **Accept plan and build on autopilot (recommended)** または、インストール済みバージョンで同様のラベルのオプションを選択します。
2. プロンプト下のモード表示が **Autopilot** になっていることを確認します。
3. Copilot が計画に従って反復し、コードを生成し、テストを実行するのを確認します。

> [!NOTE]
> 承認すると実装が直ちに開始されるため、先に計画をレビューしてください。Copilot が依存関係の不足やポート競合を報告した場合は、チェックを完了と扱う前にセットアップの問題を解決してください。

## 実装をレビューして検証する

コードが生成されたら、ほかのコードと同様にマージ前にレビューします。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードにします。モード表示が **Plan** または **Autopilot** になっていないことを確認します。
2. `/diff` を入力し、フィルター実装とテストを確認します。
3. 結果を Issue と計画中に決定した事項と比較します。
4. コードをレビューしたら、<kbd>Esc</kbd> を押して差分ビューを終了します。
5. プロジェクトのチェック出力を確認し、失敗があれば Copilot に解決を依頼します。

## 新機能を確認する

コードは問題ないように見えても、実際に動作しますか。前回と同じようにアプリを起動し、Codespaces の転送ポートでサイトを開きましょう。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces がポート `4321` を利用可能だと通知したら、**Open in Browser** を選択します。
3. カテゴリーフィルター、パブリッシャー フィルター、計画で合意した組み合わせを試します。
4. リセット動作と結果なしの動作が Issue と決定事項に一致することを確認します。
5. Codespace に戻り、Copilot に起動した開発サーバーを停止するよう依頼します。

## まとめと次のステップ

さまざまな会話モードを使って機能を構築し、レビューしました。このレッスンでは、次の作業を行いました。

- GitHub Issue から新しい Copilot 会話を開始した。
- Plan モードで要件を定義した。
- Autopilot モードで新機能を実装した。
- コードをレビューした。
- 転送されたブラウザーで機能を手動検証した。

次は、ドキュメント化されたプラクティスに従う生成コードの仕組みをさらに詳しく確認するため、[カスタム指示を使用][next-lesson]します。

## リソース

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI コマンド リファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
