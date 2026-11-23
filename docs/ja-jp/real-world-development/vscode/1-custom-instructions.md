---
title: "演習 1 - カスタム指示 (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: エージェント モード →][next-lesson]

生成 AI を使う場合、コンテキストは重要です。タスクを特定の方法で実行する必要がある場合や、Copilot が知るべき背景情報がある場合は、そのコンテキストを利用できるようにします。[指示ファイル][instruction-files]は、コード生成についてガイダンスを提供する主要な方法です。

この演習では、次の内容を学習します。

- リポジトリのカスタム指示とパス スコープの指示ファイルを通じて、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot に届く仕組みを確認する。
- 現在の指示を使ってフィルターの最初のデータ スライス (パブリッシャー ヘルパー) を生成する。
- `.github/copilot-instructions.md`にリポジトリ全体の新しい標準を追加する。
- 同じプロンプトを再実行し、生成コードが新しい標準を採用する様子を確認する。
- 指示の更新とフィルター スライスを`main`にコミットし、次の演習で更新されたガイドを利用できるようにする。

> [!CAUTION]
> 生成コードは設定した標準と完全には一致しない場合があります。Copilot は確率的に動作します。この演習の目的は、指示更新後の動作の傾向を確認することであり、文字単位で一致させることではありません。

## 指示ファイル

### シナリオ

優れた開発チームと同様に、Tailspin Toys には開発プラクティスに関するガイドラインがあります。

- データ層には常に単体テストが必要です。
- UI はダーク モードでモダンな見た目にします。
- TSDoc コメントを使ってコードにドキュメントを追加します。
- 各ファイルの先頭に目的を説明するコメント ブロックを追加します。

指示ファイルを使うことで、Copilot がこれらのプラクティスに沿った情報を利用できるようになります。

### カスタム指示

カスタム指示は、コーディング スタイルと要件を理解させるためのコンテキストと好みを Copilot に与えます。コーディング規約、ライブラリ、コメントの種類を指定できます。リポジトリ全体または特定のファイル種別に指示を作成できます。

指示ファイルには2種類あります。

- `.github/copilot-instructions.md`: リポジトリへのすべての要求に送られる単一の指示ファイル。
- `.github/instructions/*.instructions.md`: 特定の言語、ファイル種別、タスク向けのガイドラインを提供します。

> [!NOTE]
> IDE で作業する場合、指示ファイルは Copilot Chat のコード生成に使用されます。コード補完や次の編集候補には使用されません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、コード生成時にリポジトリレベルの指示と`applyTo`フロントマターを持つ指示ファイルを使用します。

### 指示ファイル管理のベストプラクティス

- `copilot-instructions.md`は、構築内容、プロジェクト構造、グローバルなコーディング標準など、プロジェクトレベルのガイダンスに絞ります。
- `*.instructions.md`は、単体テスト、Astro コンポーネント、データ層などのファイル種別や特定タスクに使用します。
- 自然言語で明確なガイダンスを示し、推奨される例と推奨されない例を示します。

## プロジェクトのカスタム指示ファイルを確認する

スターター プロジェクトには、コアの`.github/copilot-instructions.md`とさまざまなタスク向けの指示ファイルが含まれています。

1. `.github/copilot-instructions.md`を開きます。
2. プロジェクトの概要と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure**などのセクションを確認します。
3. `.github/instructions`フォルダーを開きます。Astro ファイル、Drizzle データ層、テストなどの指示があります。
4. `.github/instructions/unit-tests.instructions.md`を開き、先頭の`applyTo`フィールドを確認します。たとえば`**/*.test.ts`に一致する TypeScript テスト ファイルへ指示が適用されます。
5. `.github/instructions/drizzle.instructions.md`を開き、ほかの指示ファイルや既存ファイルへのリンクを確認します。

> [!NOTE]
> `copilot-instructions.md`の**Code formatting requirements**はコーディング標準を示していますが、コード内ドキュメントを要求していません。次の手順では、TSDoc コメントとファイル コメントヘッダーのルールを追加します。

## 変更用ブランチを作成する

1. 前の演習の Codespace に戻ります。
2. <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押して新しいターミナルを開きます。
3. 新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions
   ```

## 指示を更新する前に Copilot Chat を使用する

> [!TIP]
> **Copilot Chat を開く**
>
> Codespaceに戻り、Copilot Chat パネルを開き、**New Chat**を選択して新しい会話を開始します。

カスタム指示の影響を確認するため、まず現在の指示ファイルを使ってプロンプトを送信します。

1. 前の演習のエディター タブを閉じます。
2. `src/lib/publishers.ts`を開きます。
3. Chat ビューでエージェント ピッカーから**Agent**を選択します。

    ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

4. 次のプロンプトを送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot がプロジェクトを調査し、ヘルパー ファイルとテストを更新します。
6. 提案されるヘルパーは、`db`クライアントを最初の引数に取り、パブリッシャーの型付き配列を返す関数です。これは`.github/instructions/drizzle.instructions.md`のデータ層規約に従います。
7. 提案コードに TSDoc コメントとファイルレベルのコメントヘッダーがないことを確認します。

> [!CAUTION]
> 指示がなくても Copilot がドキュメントを追加する場合があります。その場合でも、指示更新後の一貫性の改善を確認することが目的です。

## 新しいリポジトリ標準を追加する

`.github/copilot-instructions.md`にはプロジェクトレベルの情報を記述します。リポジトリのコーディング標準をドキュメント化し、より適切なコード提案を得られるようにします。

1. `.github/copilot-instructions.md`を再度開きます。
2. 27行付近にある**Code formatting requirements**セクションを探します。
3. 既存の標準の直下に次を追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md`を保存します。

## プロンプトを再実行して変更を確認する

1. Copilot Chat に戻り、**New Chat**を選択してコンテキストをクリアします。
2. `src/lib/publishers.ts`を再度開きます。
3. 前と同じプロンプトを送信します。
4. 提案ファイルの先頭に目的を説明するコメント ブロックが追加されることを確認します。
5. 提案関数に目的、パラメーター、戻り値を説明する TSDoc コメントが含まれることを確認します。

Copilot に新しいプロジェクト標準に従わせ、次の演習で使用する実コードへ適用できました。

## 指示とブランチをコミットしてプッシュする

1. ターミナルで次を実行し、更新された指示とヘルパーの変更を確認します。

   ```bash
   git status
   ```

2. 指示と Copilot が変更した関連ファイルをステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

3. ブランチをリポジトリにプッシュします。

   ```bash
   git push -u origin custom-instructions
   ```

## pull request を作成してマージする

ブランチをプッシュしたら、pull request を作成し、バックログのドキュメント標準 Issue と関連付けます。

1. Codespace内で Copilot Chat を開きます。
2. <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) を押し、エージェント ピッカーで**Agent**を選択します。
3. 指示ファイル更新に関連する Issue を見つけ、現在のブランチから PR を作成するよう依頼します。
4. Copilot が GitHub アクションを実行する許可を求めたら、内容を確認して**Allow**を選択します。
5. PR 作成後、PR をマージし、ローカル ブランチを`main`に戻して最新コードを取得するよう依頼します。

GitHub Copilot を使って pull request を作成し、マージできました。

## まとめと次のステップ

このプロジェクトで Copilot が指示ファイルからコンテキストを取得する仕組みを確認し、VS Code の Copilot Chat を使って次の作業を行いました。

- 現在の指示を使ってコード生成プロンプトを送信し、Copilot の出力を確認した。
- `.github/copilot-instructions.md`にリポジトリ全体の新しい標準を追加した。
- 同じプロンプトを再実行し、提案コードが新しい標準を採用する様子を確認した。
- 指示の更新とヘルパーの基礎を`main`にコミットし、次の演習で利用できるようにした。

次は、その指示を使い、[エージェント モード][next-lesson]で Copilot にコードベース全体の新機能を追加させます。

## リソース

- [GitHub Copilot カスタマイズ用の指示ファイル][instruction-files]
- [カスタム指示作成のベストプラクティス][instructions-best-practices]
- [カスタム指示を改善する 5つのヒント][copilot-instructions-five-tips]
- [GitHub Copilot の個人カスタム指示][personal-instructions]
- [Awesome Copilot — 指示ファイルのコレクション][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
