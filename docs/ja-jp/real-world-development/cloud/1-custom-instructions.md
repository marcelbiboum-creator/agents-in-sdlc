---
title: "演習 1 - カスタム指示 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使う場合、コンテキストは重要です。タスクを特定の方法で実行する必要がある場合や、Copilot が知るべき背景情報がある場合は、そのコンテキストを利用できるようにする必要があります。[指示ファイル][instruction-files]は、Copilot に何をしてほしいかだけでなく、どのように実行してほしいかを伝える手段です。

この演習では、次の内容を学習します。

- リポジトリのカスタム指示とパス スコープの指示ファイルを通じて、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot に届く仕組みを確認する。
- `.github/copilot-instructions.md` にリポジトリ全体の新しい標準を追加する。

> [!NOTE]
> VS Code ハーネスや CLI ハーネスと異なり、ここでは Copilot cloud agent が GitHub Issue 上で非同期に動作するため、before/after のプロンプト比較はリアルタイムで行いません。指示ファイルの影響は、このハーネスで cloud agent が生成する pull request をレビューする際に確認します。

## 指示ファイル

### シナリオ

優れた開発チームと同様に、Tailspin Toys には開発プラクティスに関するガイドラインがあります。

- データ層には常に単体テストが必要です。
- UI はダーク モードでモダンな見た目にします。
- TSDoc コメントを使ってコードにドキュメントを追加します。
- 各ファイルの先頭に、そのファイルの目的を説明するコメント ブロックを追加します。

指示ファイルを使って、Copilot がこれらのプラクティスに沿って作業できる情報を提供します。

### カスタム指示

カスタム指示を使うと、コーディング スタイルと要件を理解させるためのコンテキストや好みを Copilot に与えられます。コーディング規約、ライブラリ、コメントの種類を指定できます。リポジトリ全体または特定のファイル種別に指示を作成できます。

指示ファイルには2種類あります。

- `.github/copilot-instructions.md`: リポジトリへの**すべての**要求に送られる単一の指示ファイル。プロジェクトレベルの情報、使用技術、構築内容の概要、ベストプラクティス、グローバルなガイダンスを記述します。
- `.github/instructions/*.instructions.md`: TypeScript、Astro、UI コンポーネント、テストなど、特定のタスクやファイル種別向けのガイドラインを提供します。

> [!NOTE]
> IDE で作業する場合、指示ファイルは Copilot Chat のコード生成に使用されます。コード補完や次の編集候補には使用されません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、コード生成時にリポジトリレベルの指示と `applyTo` フロントマターを持つ `*.instructions.md` ファイルを使用します。
>
> Copilot は AGENTS.md や CLAUDE.md など、ほかの標準を使う指示ファイルも[サポート][custom-instructions-support]しています。

### 指示ファイル管理のベストプラクティス

- `copilot-instructions.md` は、構築内容、プロジェクト構造、グローバルなコーディング標準など、プロジェクトレベルのガイダンスに絞ります。
- `*.instructions.md` は、ファイル種別 (単体テスト、Astro コンポーネント、データ層) や特定タスク向けに使用します。
- 自然言語で、明確なガイダンスと推奨される、推奨されない例を示します。

> [!TIP]
> GitHub Copilot を使うすべてのプロジェクトでは、指示ファイルを充実させることをお勧めします。[awesome-copilot][awesome-copilot]では、指示ファイル、カスタム エージェント、その他のリソースを確認できます。

## プロジェクトのカスタム指示ファイルを確認する

スターター プロジェクトには、コアの `copilot-instructions.md` とさまざまなタスク向けの `*.instructions.md` ファイルが含まれています。

1. エディターまたは GitHub Web UIで `.github/copilot-instructions.md` を開きます。
2. プロジェクトの概要と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure**などのセクションを確認します。**Code standards**の下にある **GitHub Actions Workflows**ガイダンスは、Copilotとのすべての対話に適用されます。
3. `.github/instructions`フォルダーを開きます。Astro ファイル、Drizzle データ層、テストなどの指示があります。
4. `.github/instructions/unit-tests.instructions.md`を開きます。先頭の`applyTo`フロントマターは、たとえば`**/*.test.ts`のように指示を適用するファイルを決めます。
5. `.github/instructions/drizzle.instructions.md`を開き、ほかの指示ファイルや既存ファイルへのリンクを確認します。これにより、大きな指示セットを再利用可能な小さなファイルに分割し、参照例を示せます。

> [!NOTE]
> `copilot-instructions.md`の**Code formatting requirements**はコーディング標準を示していますが、コード内ドキュメントを要求していません。次の手順では、TSDoc コメントとファイルコメントヘッダーのルールを追加します。

## 新しいリポジトリ標準を追加する

次に行うのは、ドキュメントがコード内の TSDoc コメントとファイルレベルのコメントヘッダーとして存在するようにするプロジェクト全体のルールを追加することです。cloud agent は、後続の演習で割り当てる Issue を処理するときに、この指示を読みます。

1. Codespace ターミナルから、作業ブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. `.github/copilot-instructions.md`を再度開きます。
3. **Code formatting requirements**セクションを探し、既存の標準の直下に次のMarkdownを追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md`を保存します。

> [!TIP]
> リポジトリレベルのファイルは、プロジェクト全体の標準に適しています。特定の言語、ファイル種別、タスクには`*.instructions.md`を使用します。

## 指示の更新をコミット、プッシュ、マージする

cloud agent は、Issue の対象ブランチの指示ファイルを読みます。Copilot に指示を確実に反映させるには、変更を`main`に反映します。

1. ファイルをステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.comで`custom-instructions-cloud`から`main`への pull request を作成し、マージします。次の演習で Issue を割り当てるとき、cloud agent はこの指示を読みます。

> [!TIP]
> このワークショップで`main`へ直接作業してもかまいません。その場合はブランチとコミットを省略できます。ブランチ手順は、実際のプロジェクトでの扱い方を示しています。

## まとめと次のステップ

Copilot が指示ファイルからコンテキストを取得する仕組みを確認し、`.github/copilot-instructions.md`にリポジトリ全体の新しい標準を追加しました。この標準は、このハーネスの残りの cloud agent が生成する pull request で確認します。

次は、[Copilot cloud agent に最初の Issue を割り当て][next-lesson]ます。

## リソース

- [GitHub Copilot カスタマイズ用の指示ファイル][instruction-files]
- [カスタム指示作成のベストプラクティス][instructions-best-practices]
- [カスタム指示を改善する 5 つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — 指示ファイルのコレクション][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
