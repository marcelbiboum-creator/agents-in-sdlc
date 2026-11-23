---
title: "レッスン 0 - 前提条件"
description: "Tailspin Toys の自分用コピーを作成し、Copilot CLI ワークショップで使用する GitHub Codespace を準備します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI のレッスンを始める前に、必要な準備を整えます。Tailspin Toys リポジトリの自分用コピーを作成し、[Codespace][codespaces]を起動します。次のレッスンでは、統合ターミナルを使って Copilot CLI をインストールして実行します。

このレッスンでは、次の内容を学習します。

- テンプレートから Tailspin Toys プロジェクトの自分用コピーを作成する。
- Codespace を作成し、プロジェクトの準備を確認する。

## ラボ用リポジトリを設定する

[テンプレート リポジトリ][tailspin-template]から、作業対象の Tailspin Toys プロジェクトの自分用コピーを作成します。新しいリポジトリにはラボに必要なすべてのファイルが含まれています。

1. 新しいブラウザー ウィンドウで[Tailspin Toys テンプレート][tailspin-template]を開きます。
2. **Use this template**を選択し、続いて**Create a new repository**を選択して、自分用のリポジトリを作成します。
3. GitHub または Microsoft が主催するイベントでワークショップを進めている場合は、メンターの案内に従ってください。そうでない場合は、GitHub Copilot にアクセスできる organization に新しいリポジトリを作成します。
4. 後でワークショップ内で参照するため、作成したリポジトリ パス (`organization-or-user-name/repository-name`) を控えておきます。

> [!NOTE]
> テンプレートからリポジトリを作成すると、GitHub Issue のバックログが自動的に作成されます。ワークショップ全体を通してこれらの Issue を使用するため、自分で起票する必要はありません。

ワークショップ テンプレートの新しいコピーを使用してください。リポジトリの指示、アプリケーション コード、テスト、`quality-checks` スキル、使用するバックログが含まれています。古いコピーを使用する場合は、必要なファイルが含まれているか進行役に確認してください。

## Codespace を作成する

次に Codespace を使ってワークショップを進めます。

[GitHub Codespaces][codespaces]は、ブラウザーから直接コードの作成、実行、デバッグができるクラウドベースの開発環境です。複数のプログラミング言語、拡張機能、ツールに対応したフル機能のエディターを提供します。

1. 新しく作成したリポジトリに移動します。
2. **Code**を選択します。
3. **Codespaces**タブを選択し、**Create codespace on main**を選択します。
4. Codespace のセットアップが完了するまで待ちます。テンプレートによって、プロジェクトの依存関係、Playwright Chromium、ローカル データベースがインストールされます。
5. **Do you trust the authors of the files in this folder?**と表示されたら、**Trust Folder & Continue**を選択します。
6. リポジトリのルートでターミナルを開き、アプリケーションを起動します。

   ```bash
   npm run dev
   ```

7. Codespaces がポート `4321` を利用可能だと通知したら、**Open in Browser**を選択し、Tailspin Toys サイトが読み込まれることを確認します。
8. ターミナルに戻り、<kbd>Ctrl</kbd>+<kbd>C</kbd>を押して開発サーバーを停止します。

## まとめと次のステップ

準備が整いました。このレッスンでは、次の作業を行いました。

- テンプレートから Tailspin Toys プロジェクトの自分用コピーを作成した。
- Codespace を作成し、プロジェクトの準備を確認した。

次は、Codespace に[GitHub Copilot CLI をインストール][next-lesson]し、GitHub アカウントで認証します。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces の概要][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-install-copilot-cli/
[codespaces]: https://github.com/features/codespaces
