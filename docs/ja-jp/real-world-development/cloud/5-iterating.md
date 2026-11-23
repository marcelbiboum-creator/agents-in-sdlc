---
title: "演習 5: GitHub Copilot の作業を反復改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

このラボでは、ユーザー体験の改善と機能追加を目的に GitHub Copilot の作業を使いました。Copilot にドキュメント追加、デザインチーム向けの関連ゲーム機能、ハイコントラスト モードとライト モードのアクセシビリティ機能の実装を依頼しました。次にコード変更を確認し、必要に応じてフィードバックを送り、Copilot の成果を改善します。

### シナリオ

生成 AI を使用しても、ソフトウェア設計と DevOps の基本は変わりません。生成されたコードを常にレビューし、通常の DevOps プロセスを実行します。ドキュメント、関連ゲーム、アクセシビリティ機能の提案を確認してから、チームのほかのメンバーにレビューを依頼しましょう。

## セキュリティと Copilot cloud agent

Copilot cloud agent は監視なしで非同期に作業するため、安全性を確保するセキュリティ制約があります。

- Copilot はリポジトリへの読み取り専用アクセスと、コードを変更するブランチへの書き込み専用アクセスを持ちます。
- cloud agent は GitHub Actions 内で実行され、独立したエフェメラル環境を作成します。
- GitHub Actions ワークフローを実行するには、人間の承認が必要です。
- [外部リソースへのアクセスは既定で制限][agent-firewall]され、MCP serverも含みます。

## 生成されたドキュメントをレビューする

最初の GitHub Copilot cloud agent の pull requestから確認します。対象はコードへのドキュメント追加です。github.comの標準的な PR インターフェイスを使います。

> [!NOTE]
> PR を確認すると、Copilot がファイアウォールでブロックされたという警告が表示される場合があります。これは想定内です。Copilot は外部リソース、外部 MCP serverへの呼び出しを含め、既定でアクセスが制限されています。必要に応じて[cloud agent のファイアウォールをカスタマイズまたは無効化][agent-firewall]できます。

1. github.comでリポジトリに戻ります。
2. **Pull Requests**を選択して一覧を開きます。
3. `Add missing documentation`または類似のタイトルを持つ pull request を開きます。

> [!NOTE]
> Copilot がまだ作業中の場合、pull requestには**[WIP]**フラグがあります。完了まで数分待ちます。

4. **Files changed**タブを選択し、変更を確認します。

    ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. 新しく作成された TSDoc コメントやほかのドキュメントを含む更新コードを確認します。正確な変更は異なる場合があります。
6. TSDoc コメント、TypeScript の規約、コメントヘッダーを確認します。これらは演習 2で確認したカスタム指示ファイルから導かれます。
7. 更新が問題ないことを確認したら、**Conversation**タブに戻って下へスクロールします。
8. 承認待ちのワークフローがある場合は、**Approve and run workflows**を選択します。

   ![ワークフローの承認と実行](../../../_images/shared-approve-workflows.png)

9. pull request のチェックセクションにワークフローがキューされます。問題がなければ、単一の Astro アプリのプロジェクトチェックが成功します。

## Copilot に変更を依頼する

pull request で Copilot と協働するのは一方的な作業ではありません。pull request のコメントやコードのインライン コメントで`@copilot`をタグ付けすると、Copilot が新しいセッションを開始して対応します。たとえば、次の変更を依頼できます。

- 各コード ファイルの先頭に、目的を説明するコメントヘッダーを追加する。
- TypeScript ファイルと Astro ファイルに TSDoc コメントを追加する。
- Astro アプリの構造を説明する README を作成する。

1. 生成されたドキュメントに変更を依頼し、ほかのユーザーと同じように`@copilot`をタグ付けします。
2. **View Session**を選択し、Copilot が更新を実行する様子を確認します。
3. **Back to pull request**を選択して PR に戻ります。

    ![pull requestに戻る](../../../_images/ex7-back-to-pr.png)

4. Copilot が変更を完了すると、PR に新しいコミットが表示されます。
5. **Files changed**タブで変更をレビューします。

満足するまで反復します。満足したら draft を ready に変更し、`main`ブランチへマージします。

## 関連ゲーム機能をレビューする

ゲーム詳細ページに関連ゲームを表示する Issue 用に Copilot が生成した PR を確認します。

1. GitHub.comでリポジトリに戻ります。
2. **Pull Requests**タブを選択します。
3. `Show related games on the game details page`に似たタイトルの PR を選択します。
4. **Files changed**タブで生成されたコードを確認します。
5. 更新が問題なければ、**Conversation**タブに戻り、承認待ちのワークフローがあるか確認します。
6. ワークフローが承認待ちの場合は、**Approve and run workflows**を選択します。
7. チェックが成功し、単一の Astro アプリのテストが通ることを確認します。
8. **省略可能:** Codespaceでブランチを切り替え、関連ゲーム機能を手動テストできます。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot cloud agent の作業は反復可能です。表示する関連ゲームの件数を調整したり、カスタム指示によるコメントヘッダーや TSDoc コメントの追加を依頼したりできます。Conversation タブにコメントを追加すると、新しいセッションが開始されます。

## アクセシビリティ機能をレビューする

最後に、カスタムアクセシビリティ エージェントが実装した機能を確認します。演習 3で割り当てたハイコントラスト モードと、演習 4でリクエストしたライト モードが含まれているはずです。

1. リポジトリに戻ります。
2. **Pull Requests**タブを選択します。
3. `Add high contrast mode to website`に似たタイトルの PR を選択します。
4. **Files changed**タブで生成されたコードを確認します。
5. 特に次の点を確認します。
   - モード切り替え UI コンポーネント。
   - ユーザー設定を永続化するローカルストレージ。
   - ハイコントラスト モードとライト モードの CSS またはスタイル変更。
   - アクセシビリティ属性 (ARIA ラベル、キーボード ナビゲーションなど)。
   - モード切り替えを管理する JavaScript/TypeScript。

6. 問題がなければ Conversation タブに戻り、承認待ちのワークフローを確認します。
7. **Approve and run workflows**を選択し、すべてのチェックを完了させます。
8. **省略可能:** Codespaceでブランチを切り替え、ブラウザーからハイコントラスト モードとライト モードをテストし、ページ更新後も設定が保持されることを確認します。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

カスタムアクセシビリティ エージェントが、アクセシビリティのベストプラクティスに沿った実装を Copilot にガイドしました。懸念がある場合は、前の PR と同様に`@copilot`をタグ付けして更新を依頼できます。

## 任意の演習 - 委任を続ける

cloud agent は、実際のバックログ項目を任せられるときに最も効果的です。リポジトリに Issue を追加し、Copilot に割り当てることを検討してください。

- ゲーム詳細ページに支援者関心フォームを作成する。
- ゲーム一覧ページにページネーションを実装する。
- データアクセスヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent ハーネスを完了しました。このレッスンでは、次の作業を行いました。

- リポジトリのカスタム指示ファイルを確認し、cloud agent の出力への影響を把握した。
- Issue を Copilot cloud agent に割り当て、環境セットアップ、計画、非同期実行を確認した。
- アクセシビリティ用カスタム エージェントを作成して使用し、ハイコントラストモードとライトモードを追加した。
- エージェント ページを Mission controlとして使い、アクセシビリティ セッションを監視して進行中に方向付けした。
- cloud agent の pull requestをレビューし、反復改善し、`@copilot`で変更を依頼し、ワークフローを承認した。

## 振り返りと次のステップ

Cloud agent ハーネスを完了しました。ほかのハーネスでは関連するシナリオを扱います。

- 🖥️ **[VS Code ハーネス](../../vscode/)** - エディター内で Copilot Chat エージェント モードと MCP 統合を確認します。
- 💻 **[CLI ハーネス](../../cli/)** - ターミナルからレビュー済みの変更を2つ提供し、Plan モード、Autopilot モード、エージェント スキル、カスタム QA エージェント、Playwright MCP を使用します。

自分のリポジトリでは、次のことを試せます。

- リファクタリングやテスト カバレッジ向上の Issue を cloud agent に割り当てる。
- 別のドメイン向けカスタム エージェントを作成する。
- ほかのスタック向けに`copilot-setup-steps.yml`を設定する。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot エージェントの概要][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent セットアップ ワークフローのベストプラクティス][cloud-agent-best-practices]
- [Copilot cloud agent ファイアウォールの構成][agent-firewall]

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[previous-lesson]: ../4-managing-agents/
[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
