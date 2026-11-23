---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前の演習では、Copilot cloud agent にユーザー体験の改善と機能追加という3つのタスクを依頼しました。cloud agent は非同期かつ自律的に動作しますが、タスクを監視できることも重要です。

github.comの[エージェント ページ][agents-page]など、cloud agent に割り当てたタスクを管理するツールがあります。Mission controlから、オープンな pull requestを持つすべてのエージェント タスクを確認し、実行された操作を調べ、進行中のセッションを方向付けして追加ガイダンスを与えられます。

このレッスンでは、次の内容を学習します。

- エージェント ページを確認して cloud agent タスクを監視する。
- 進行中のセッションを方向付けして追加機能を依頼する。

## シナリオ

ハイコントラスト モードの作成をエージェントに依頼した後、チームはライト モードを追加するのがよいタイミングだと判断しました。サイトのスタイル更新と切り替え機能の実装を進めているので、ハイコントラストに加えてライト モードも追加するようエージェントの作業を方向付けます。

## Copilot cloud agent のタスクを確認する

Copilot cloud agentに割り当てたタスクの現在の状態を確認します。

1. [Copilot エージェント ページ](https://github.com/copilot/agents)に移動します。
2. メイン ペインと左ペインにタスク一覧が表示されます。割り当てたタスクは次のようなものです。
   - コードベースのドキュメント更新。
   - ゲーム変更用 API の生成。
   - Web サイトへのハイコントラスト モード追加。
3. 実行中のタスクを選択し、Copilot が実行したタスクを確認します。
4.右側の pull request ペインで PR と変更ファイルを確認します。

> [!NOTE]
> 表示される手順は、Copilot の作業状況と採用したアプローチによって異なります。

## cloud agent を方向付ける

ハイコントラスト モードの作業中にライト モード切り替えも追加するよう依頼します。

1. ハイコントラスト モード追加に関するセッションを選択します。
2. セットアップが完了し、作業を開始したことを示すメッセージになるまで数分間確認します。
3. **Steer active session while Copilot is working**ダイアログに次のプロンプトを入力します。

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

4. <kbd>Enter</kbd>でプロンプトを送信します。
5. Copilot がプロンプトを認識し、作業フローに組み込むことを確認します。

## Copilot の作業を待つ

更新されたタスクへの作業を Copilot が開始します。送信時に作業中の特定ステップが完了してから、新しい要求が反映されます。

## まとめと次のステップ

このレッスンでは、Copilot cloud agent タスクを監視し、進行中のセッションを方向付ける Mission controlとしてエージェント ページを確認しました。アクティブなタスクと完了したタスクを追跡し、作業をレビューし、追加ガイダンスで進行中のタスクを調整できました。

次は、[Copilot が作成した pull requestを反復改善][next-lesson]します。

## リソース

- [Copilot エージェント ページ][agents-page]
- [カスタム エージェントの概要][custom-agents]

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
