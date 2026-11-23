---
title: "レッスン 0 - 前提条件"
description: "GitHub Copilot app のレッスンに向けて、Tailspin Toys プロジェクト用の Node.js をインストールし、テンプレートからリポジトリの自分用コピーを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

GitHub Copilot app は、Copilot と GitHub を一元的に扱うデスクトップ アプリです。Issue や pull request にすばやくアクセスでき、GitHub Copilot を使った開発も行えます。このワークショップでは、Astro で構築された Tailspin Toys アプリを GitHub Copilot app を使ってローカルで更新します。開始前に Node.js がローカルにインストールされていることを確認し、Copilot app をインストールします。

このレッスンでは、次の内容を学習します。

- プロジェクトのテストを実行できるよう、Node.js をインストールする。
- テンプレートから Tailspin Toys プロジェクトの自分用コピーを作成する。

## Node.js をインストールする

いくつかのレッスンでは、エージェントに機能を構築させ、Tailspin Toys のテストスイートをローカルで実行します。そのためには、プロジェクトが必要とする唯一のランタイムである [**Node.js**][nodejs]が必要です。現在の **LTS** リリースをインストールしてください。

どのプラットフォームでも公式インストーラーを使うのが最も簡単です。

1. 使用しているオペレーティング システムで、Windows Terminal、macOS のターミナルなど、普段使うターミナルを開きます。
2. 次のコマンドを実行し、インストールされている Node.js のバージョンを確認します。

    ```shell
    node --version
    npm --version
    ```

3. どちらのコマンドも成功し、プロジェクトの README と `package.json` が必要とする要件を Node.js が満たしている場合は、次のセクションに進めます。

> [!TIP]
> Node.js がインストールされていない場合、または更新が必要な場合にのみ、以降の手順を実行してください。

4. [Node.js のダウンロード ページ][node-download]を開きます。
5. 使用するオペレーティング システム向けの **LTS** ビルドをダウンロードします。
6. インストーラーを実行し、既定の設定を受け入れます。Windows では **Add to PATH** を選択したままにします。
7. インストールが完了したら、新しいターミナル ウィンドウを開きます。
8. 新しいターミナル ウィンドウで次を実行し、インストールを確認します。

    ```bash
    node --version
    npm --version
    ```

9. インストールされた Node.js と npm のバージョンが表示されるはずです。

> [!IMPORTANT]
> Copilot app のエージェントからも `node --version` と `npm --version` を実行できる必要があります。普段使うターミナルで成功していても、appから利用できるとは限りません。Node.js をインストールした後、または PATH を変更した後は、appを完全に終了して再起動してください。セッションでどちらかのコマンドが失敗する場合は、続行前に[セッション環境のトラブルシューティング][session-environment]に従ってください。

> [!IMPORTANT]
> 各 worktreeにも、プロジェクトの依存関係と E2E チェック用の Playwright Chromium が必要です。worktree の準備では Tailspin Toys リポジトリの README に従い、インストール要求は承認前に確認してください。

## ラボ用リポジトリを設定する

Tailspin Toys プロジェクトの自分用コピーを使って作業します。[テンプレート リポジトリ][template-repository]から作成してください。新しいリポジトリにはラボに必要なすべてのファイルが含まれ、appのインストール時に接続します。

1. 新しいブラウザー ウィンドウで、このラボの GitHub リポジトリ `https://github.com/github-samples/tailspin-toys` を開きます。
2. ラボ リポジトリ ページで **Use this template** ボタンを選択し、**Create a new repository**を選択して、自分用のリポジトリを作成します。

    ![ドロップダウンで Create a new repository が選択された Use this template ボタン](../../../_images/app-0-use-template.png)

3. GitHub または Microsoft が主催するイベントでワークショップを進めている場合は、メンターの案内に従ってください。そうでない場合は、GitHub Copilot にアクセスできる organization にリポジトリを作成できます。

    ![テンプレートに github-samples/tailspin-toys が設定され、リポジトリ名が入力された Create a new repository フォーム](../../../_images/app-0-create-repository.png)

4. 作成したリポジトリ パス (**organization-or-user-name/repository-name**) を控えておきます。このラボで後ほど参照します。

> [!NOTE]
> テンプレートからリポジトリを作成すると、GitHub Issue のバックログが自動的に作成されます。ワークショップ全体を通してこれらの Issue を使用するため、自分で起票する必要はありません。

ワークショップ テンプレートの新しいコピーを使用してください。リポジトリの指示、アプリケーション コード、テスト、quality-checks スキル、既存のキャンバス拡張機能が含まれています。ワークショップ中にスキルをカスタマイズし、QA エージェントを作成します。古いコピーを使用する場合は、必要なファイルが含まれているか進行役に確認してください。

## まとめと次のステップ

準備が整いました。このレッスンでは、次の作業を行いました。

- プロジェクトをローカルでビルドしてテストできるよう Node.js をインストールした。
- テンプレートから Tailspin Toys リポジトリの自分用コピーを作成した。

次は、[GitHub Copilot app をインストール][next-lesson]し、作成したリポジトリを接続してワークスペースを確認します。

## リソース

- [Node.js のダウンロード][node-download]
- [テンプレートからリポジトリを作成する][template-repository]
- [GitHub Copilot app の概要][about-copilot-app]

[next-lesson]: ../1-install-copilot-app/
[nodejs]: https://nodejs.org/
[node-download]: https://nodejs.org/en/download
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[session-environment]: ../3-agent-modes/#start-a-session-from-the-issue
