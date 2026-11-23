---
title: "演習 0: 前提条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

VS Code の演習を始める前に、必要な準備を整えます。Tailspin Toys リポジトリの自分用コピーを作成し、作業用の[codespace][codespaces]を起動し、エディターで GitHub Copilot Chat が動作することを確認します。

## ラボ用リポジトリを設定する

作成するコード用リポジトリのコピーを作成するには、[テンプレート][template-repository]からインスタンスを作成します。新しいインスタンスにはラボに必要なファイルがすべて含まれ、演習を進める間使用します。

1. 新しいブラウザー ウィンドウで[Tailspin Toys テンプレート][tailspin-template]を開きます。
2. ラボ リポジトリ ページで **Use this template**ボタンを選択し、自分用のリポジトリを作成します。続いて**Create a new repository**を選択します。

    ![「Use this template」ボタン](../../../_images/ex0-use-template.png)

3. GitHub または Microsoft が主催するイベントでワークショップを進めている場合は、メンターの案内に従ってください。そうでない場合は、GitHub Copilot にアクセスできる organization にリポジトリを作成できます。

    ![リポジトリ テンプレートの設定を入力する画面](../../../_images/ex0-repository-settings.png)

4. 後で参照するリポジトリ パス (**organization-or-user-name/repository-name**) を控えておきます。

> [!NOTE]
> **バックログの準備は完了しています**
>
> テンプレートからリポジトリを作成すると、GitHub Issue のバックログが自動的に作成されます。ワークショップ全体を通してこれらの Issue を使って作業します。

## Codespace を作成する

次に Codespace を使ってラボの演習を進めます。

[GitHub Codespaces][codespaces]は、ブラウザーから直接コードの作成、実行、デバッグができるクラウドベースの開発環境です。複数のプログラミング言語、拡張機能、ツールに対応した完全な IDE を提供します。

1. 新しく作成したリポジトリに移動します。
2. 緑色の **Code**ボタンを選択します。

    ![「Code」ボタンを選択する](../../../_images/ex0-code-button.png)

3. **Codespaces**タブを選択し、**+**ボタンで新しい Codespace を作成します。

    ![新しい Codespace を作成する](../../../_images/ex0-create-codespace.png)

Codespace の作成には数分かかりますが、すべてのサービスを手動でインストールするよりはるかに速いです。待っている間に、次の演習で使う GitHub Copilot の機能を確認できます。

> [!CAUTION]
> 後続の演習で codespace に戻ります。いまはブラウザーのタブで開いたままにしてください。

> [!NOTE]
> このワークショップは Codespace またはローカルの[dev container][dev-containers]内で実行できます。どちらもスムーズな体験に必要な前提条件を備えています。ローカルで実行する場合は、クローンしたリポジトリを VS Code で開き、表示されたら**Reopen in Container**を選択してください。VS Code が Codespace と同じ dev container を構築します。

## GitHub Copilot Chat とエージェント モードを使用する

GitHub Copilot Chat のエージェント モードを利用するには、IDE に GitHub Copilot Chat 拡張機能がインストールされている必要があります。GitHub Codespaceを使用している場合は、すでにインストールされているはずです。

> [!TIP]
> GitHub Copilot Chat 拡張機能がない場合は、[Visual Studio Code Marketplace][copilot-chat-extension]からインストールできます。または VS Code の拡張機能ビューを開き、**GitHub Copilot Chat**を検索して**Install**を選択します。

拡張機能をインストールした後、GitHub アカウントで認証して有効化する必要がある場合があります。

1. Codespace に戻ります。
2. エディター右側に Copilot Chat が表示されていない場合は、Codespace上部の Copilot Chat アイコンを選択します。
3. Copilot Chat ウィンドウに「Hello world」のようなメッセージを入力し、<kbd>Enter</kbd>を押します。Copilot Chat が起動します。
4. 認証済みでない場合は、GitHub アカウントへのサインインを求められます。案内に従って認証します。

    ![Copilot Chat 認証プロンプトの例](../../../_images/ex1-copilot-authentication.png)

5. 認証後、Copilot Chat ウィンドウが表示されます。

## まとめ

ラボ リポジトリのコピーを作成し、コードを作成するときに使用する Codespace の作成を開始しました。

## 次のステップ

Copilot にプロジェクトの規約を教えるため、[演習 1 - カスタム指示][next-lesson]に進んでください。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces クイックスタート][codespaces-quickstart]

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
