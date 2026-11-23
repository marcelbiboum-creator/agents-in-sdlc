---
title: "演習 4 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]は、開発ワークフロー内の特定タスクやドメイン向けに作成できる専門的な AI アシスタントです。リポジトリの`.github/agents`フォルダーに Markdown ファイルを定義すると、特定の作業を効果的に実行するための指示、ベストプラクティス、コーディング パターン、ドメイン知識を Copilot に与えられます。[WCAG][wcag]準拠を徹底するアクセシビリティ エージェント、安全なコーディング プラクティスに従うセキュリティ エージェント、一貫したテスト パターンを維持するテスト エージェントなどを作成できます。

カスタム エージェントは、プロジェクトの`.github/agents`フォルダーまたはグローバルな`~/.copilot/agents`で定義します。各ファイルには少なくとも`name`と`description`を含む YAML フロントマターがあり、その後にエージェントの動作、専門知識、指示を定義する Markdown プロンプトがあります。

### カスタム エージェントとエージェント スキルの違い

カスタム エージェントと[エージェント スキル][agent-skills-concept]には重複があります。どちらも Markdown ファイルで定義し、AI に操作方法を伝えます。単純に分けると、**カスタム エージェント**は作業者、**スキル**はツールです。

カスタム エージェントには独自のコンテキスト ウィンドウがあり、スキルやほかのエージェントを調整できます。このラボでは、アクセシビリティ カスタム エージェントがガイドラインに沿ってサイトをレビューして更新します。

> [!NOTE]
> カスタム エージェントの作成方法に唯一の正解はありません。環境とシナリオに合うものをテストして反復改善してください。

## シナリオ

Tailspin Toys は、視覚的な能力や好みに関係なく、すべてのユーザーがクラウドファンディング プラットフォームを利用できるように取り組んでいます。テキストと背景のコントラストが不十分なため、一部のユーザーは現在のダーク テーマを読みづらいと感じています。デザイン チームは、ユーザーがオン/オフできるハイコントラスト モードを実装するよう求めています。

アクセシビリティは重要なため、迅速に実装する必要があります。カスタム エージェントを使って機能を生成します。

この演習では、次の内容を学習します。

- 既存のアクセシビリティ カスタム エージェントを確認する。
- Copilot Chatでアクセシビリティ エージェントを使い、ハイコントラスト モードを実装する。

## アクセシビリティ カスタム エージェントを確認する

アクセシビリティ用のカスタム エージェントがすでに作成されています。

Codespaceに戻り、ターミナルを開いて、アクセシビリティ作業用に`main`から新しいブランチを作成します。演習 3のフィルター PRとは別に進めます。

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. `.github/agents/accessibility.md`を開きます。
2. `name`と`description`フィールドを含む YAML フロントマターを確認します。

> [!CAUTION]
> カスタム エージェントでは、`name`と`description`を含むフロントマターが必要です。

3. 次のセクションを確認します。
   - アクセシブルな Web サイトを生成する際の主要な責務。
   - アクセシビリティのベストプラクティス。
   - HTML、CSS、JavaScript のコード例。
   - よくある落とし穴と誤りの一覧。

## Copilot Chatでカスタム エージェントを使用する

VS Codeは、`.github/agents`で定義されたすべてのカスタム エージェントを Copilot Chatビュー下部のエージェント ピッカーに表示します。

> [!TIP]
> **Copilot Chat を開く**
>
> Codespaceに戻り、Copilot Chat パネルを開き、**New Chat**で新しい会話を開始します。

1. Chatビューのエージェント ピッカーで**Agent**を選択します。

   ![Chatビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

2. チャットビュー下部のエージェント ピッカーを選択します。既定では**default**が表示されています。
3. 利用可能なエージェント一覧から**Accessibility agent**を選択します。
4. アクセシビリティ エージェントに次のプロンプトを送信します。

    ```plaintext
    Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
    ```

5. Copilot Chat がコードベースを調査し、変更案を提示し、プロジェクト ファイルを編集します。各編集はファイル パスと差分付きでチャット内に表示されます。
6. **Files changed**インジケーターが更新され、エージェントが変更したファイル一覧を確認できます。

> [!NOTE]
> 処理には数分かかる場合があります。Copilot は、Astro コンポーネント、CSS、関連テストなどの既存ファイルを更新します。

この進行中の作業は次の演習でレビューして方向付けします。

## まとめと次のステップ

このレッスンでは、特定タスクやドメイン向けの専門 AI アシスタントである GitHub Copilot の[カスタム エージェント][custom-agents]を確認しました。

- カスタム エージェントの定義方法。
- Copilot Chat エージェント モードでカスタム エージェントを使用する方法。

次は、[エージェントの作業を監視して方向付け][next-lesson]し、変更を確認しながらライト モード切り替えを追加します。

## リソース

- [カスタム エージェントの概要][custom-agents]
- [IDEでカスタム エージェントを作成する][creating-custom-agents-ide]
- [VS Codeのカスタム エージェント][custom-agents-vscode]
- [カスタム エージェントの構成][custom-agents-config]

| [← 前のレッスン: Playwright MCP serverでフィルター機能をテストする][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
