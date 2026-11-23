---
title: "レッスン 12 - GitHub Pages でサイトを公開する"
description: "GitHub Copilot app を使って Pages ワークフローを設定し、pull request をレビューして、公開された Space Quiz を確認します。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

GitHub Pages を使って Space Quiz を公開し、一般公開します。Copilot はワークフローの準備と公開手順を案内できますが、変更をレビューし、サイトが公開されていることを確認するのは学習者の責任です。

このレッスンでは、次の内容を学習します。

- Copilot に GitHub Pages のデプロイ設定を依頼する。
- マージ前にワークフローと pull request をレビューする。
- デプロイを追跡し、公開されたサイトを確認する。

## シナリオ

Space Quiz はすでに GitHub リポジトリにありますが、簡単に試せる公開方法が必要です。単一ファイルのサイトを GitHub Pages に公開すると、サーバーやランタイムの依存関係を追加せずに、一般の URL から利用できるようになります。

## Copilot にデプロイを準備させる

> [!WARNING]
> pull request を作成すると、コードがコミットおよびプッシュされる場合があります。プロンプトを送信する前に、承認設定とデプロイ先リポジトリを確認してください。**Approve all** を使用すると、個別の確認プロンプトが表示されないことがあります。

`space-quiz` の Copilot app セッションで、次のプロンプトを送信します。

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## ワークフローと pull request をレビューする

1. リポジトリに README がない場合だけ、README が追加されることを確認します。
2. ビルドとデプロイの手順、トリガー、権限を含め、pull request の変更をレビューします。
3. ワークフローが、未マージの pull requestではなく既定ブランチからデプロイすることを確認します。
4. 必要な修正を依頼し、更新された差分をレビューします。マージを承認する前に、必要な pull request チェックがすべて成功するまで待ちます。

## マージとデプロイを承認する

> [!WARNING]
> 次のプロンプトは、レビュー済みの pull request のマージ、リポジトリの Pages 設定変更、サイトの公開をエージェントに承認するものです。レビューが完了し、リポジトリと pull request を確認した後だけ送信してください。承認設定によっては、これらの操作時に追加の確認プロンプトが表示されない場合があります。

`<PR_NUMBER>` をレビューした pull request の番号に置き換えて、別のプロンプトを送信します。

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![マージされた Space Quiz pull request、Build website、Upload artifact、Deploy to Pages の手順を含む GitHub Actions の Deploy website 実行、公開された `yourname.github.io/space-quiz/` の 3 段階を示した図。](../../../_images/first-steps-app-pages-deploy.svg)

## デプロイを確認する

1. GitHub Actions のデプロイ実行を完了まで確認します。
2. 報告された URL を開き、Space Quiz が読み込まれることを確認します。

エージェントが Pages を有効にするか pull request をマージできない場合は、提示された具体的な手順に従います。デプロイが完了し、公開されたサイトが読み込まれるまで、このタスクを完了として扱わないでください。

## まとめと次のステップ

Space Quiz を公開されたサイトとして利用できるようになり、エージェントの報告だけでなくデプロイ自体を確認しました。[レッスン 13: 振り返りと次のステップ][next-lesson]に進んでください。

[next-lesson]: ../13-review/
