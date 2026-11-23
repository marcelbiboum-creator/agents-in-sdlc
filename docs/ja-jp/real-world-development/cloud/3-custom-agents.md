---
title: "演習 3 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]は、開発ワークフロー内の特定タスクやドメイン向けに作成できる専門的な AI アシスタントです。リポジトリの`.github/agents`フォルダーに Markdown ファイルを定義すると、特定の作業を効果的に実行するための指示、ベストプラクティス、コーディング パターン、ドメイン知識を Copilot に与えられます。チームは[WCAG][wcag]準拠を徹底するアクセシビリティ エージェント、安全なコーディング プラクティスに従うセキュリティ エージェント、一貫したテスト パターンを維持するテスト エージェントなど、専門知識を再利用可能なエージェントにすることができます。

カスタム エージェントは、プロジェクトの`.github/agents`フォルダーまたはグローバルな`~/.copilot/agents`で定義されます。各ファイルには少なくとも`name`と`description`を含む YAML フロントマターがあり、その後にエージェントの動作、専門知識、指示を定義する Markdown プロンプトがあります。

### カスタム エージェントとエージェント スキルの違い

カスタム エージェントと[エージェント スキル][agent-skills-concept]には重複があります。どちらも主に Markdown ファイルで定義され、AI に操作方法を伝えます。単純に分けると、**カスタム エージェント**は作業者、**スキル**はツールです。

カスタム エージェントには独自のコンテキスト ウィンドウがあり、作業時にスキルやほかのエージェントを調整できます。このラボでは、アクセシビリティ カスタム エージェントがアクセシビリティ ガイドラインに沿ってサイトをレビューして更新します。その過程で pull request ワークフロー スキルやテスト実行スキルを呼び出せます。

> [!NOTE]
> カスタム エージェントの作成方法に唯一の正解はありません。環境とシナリオに合うものをテストして反復改善してください。

この演習では、次の内容を確認します。

- カスタム エージェントの定義方法。
- タスクをカスタム エージェントに割り当てる方法。

## シナリオ

Tailspin Toys は、視覚的な能力や好みに関係なく、すべてのユーザーがクラウドファンディング プラットフォームを利用できるように取り組んでいます。最近のフィードバックでは、テキストと背景のコントラストが不十分なため、現在のダークテーマが読みづらいという声がありました。デザイン チームは、ユーザーがオン/オフできるハイコントラスト モードを実装するよう求めています。

アクセシビリティは重要なため、迅速に実装できることが求められます。カスタム エージェントを使って機能を生成します。

## アクセシビリティ カスタム エージェントを確認する

アクセシビリティ用のカスタム エージェントがすでに作成されています。Copilot がどのようにガイドするか理解するため、内容を確認します。

1. Codespace に戻り、`.github/agents/accessibility.md`を開きます。
2. `name`と`description`フィールドを含む YAML フロントマターを確認します。

> [!CAUTION]
> カスタム エージェントでは、`name`と`description`を含むフロントマターが必要です。

3. 次のセクションを確認します。
   - アクセシブルな Web サイトを生成する際の主要な責務。
   - アクセシビリティのベストプラクティス。
   - HTML、CSS、JavaScript のコード例。
   - よくある落とし穴と誤りの一覧。

## Issue を作成して割り当てる

Mission control は環境内のすべてのエージェントを操作する中心的な場所です。タスクを Copilot cloud agent に割り当て、タスクを監視し、方向を変更して追加ガイダンスを提供できます。ここでは、ハイコントラスト モードの作成タスクを Copilot に割り当てます。

1. リポジトリに移動します。
2. **Issues**タブを選択します。
3. **New issue**を選択し、新しい Issue ダイアログを開きます。
4. **Blank issue**を選択します。
5. タイトルを`Add high contrast mode to website`に設定します。
6. 説明に次を設定します。

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. **Create**を選択します。
8. 右側の **Assign to Copilot**を選択します。
9. カスタム エージェント一覧から **Accessibility agent**を選択します。

    ![カスタム エージェントとアクセシビリティを強調した cloud agent の割り当て画面](../../../_images/ex5-select-custom-agent.png)

10. **Assign**を選択します。
11. Copilot がバックグラウンドでタスクを開始します。

## まとめと次のステップ

このレッスンでは、GitHub Copilot の[カスタム エージェント][custom-agents]を確認しました。カスタム エージェントは、特定タスクやドメイン向けの専門 AI アシスタントです。チームの専門知識と標準を再利用可能なエージェントにまとめ、特定の作業を効果的に実行させられます。

次は、Mission controlからセッションを[監視して方向付け][next-lesson]します。

## リソース

- [カスタム エージェントの概要][custom-agents]
- [organizationでカスタム エージェントを使う準備][org-custom-agents]
- [enterpriseでカスタム エージェントを使う準備][enterprise-custom-agents]

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
