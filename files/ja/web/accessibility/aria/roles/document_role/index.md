---
title: "ARIA: document ロール"
slug: Web/Accessibility/ARIA/Roles/document_role
---

複雑な複合[ウィジェット](/ja/docs/Web/Accessibility/ARIA/Roles/widget_Role)や[アプリケーション](/ja/docs/Web/Accessibility/ARIA/Roles/Application_Role)で一般的に使用される文書 (`document`) ロールは、コンテキストを読み取りモードに切り替えることを支援技術を知らせることができます。 文書 (`document`) ロールは、読み取りモードまたは閲覧モードを持つ支援技術に、この要素に含まれるコンテンツを文書モードを使用して読み取るように指示します。

```html
<div role="dialog">
  ...
  <div id="InfoText" role="document" tabindex="0">
    <p>いくつかの情報テキストがここに入ります。</p>
  </div>
  ...
  <button>閉じる</button>
</div>
```

この例は、いくつかのコントロールと、支援技術のユーザーがタブ移動で読むことができる情報テキストを含むセクションを備えた[ダイアログ](/ja/docs/Web/Accessibility/ARIA/Roles/dialog_role)ウィジェットを示しています。

## 説明

デフォルトでは、ウェブページは文書 (document、ドキュメント) として扱われ、支援技術 (AT) は、新しいウェブページに入るとき閲覧モードまたは読み取りモードにします。 このモードは、ウィジェットロールやアプリケーション (`application`) ロールなど、さまざまなロールを通じて変更できます。 文書 (`document`) ロールは、AT を閲覧モードまたは読み取りモードに戻します。

一般的に、アプリケーションロールまたは他のインタラクティブなウィジェットロール内に配置される文書 (`document`) ロールは、利用可能な場合、支援技術のユーザーが閲覧モードまたは仮想読み取りモードを使用して読むべきである複雑な複合ウィジェットのセクションを示すために使用します。

読み取りモードを持つ AT は、ウィジェットロールまたはアプリケーションロールの設定を持つ要素を除くすべての要素に対して読み取りモードをデフォルトとしているため、文書ロールは、静的リッチテキストとして読むべきであるウィジェットまたはアプリケーション内のフォーカス可能な要素に対してのみ役立ちます。 ウィジェット内のテキストを含む要素に `role="document"` と `tabindex="0"` を追加すると、スクリーンリーダーのユーザーは <kbd>Tab</kbd> キーを押して文書要素にフォーカスを置き、スクリーンリーダーの読み取りカーソルでテキストを読むことができます。

支援技術は、コンテキストを文書モードに戻すべきであり、場合によっては、親の動的コンテキスト用に配線されたコントロールから横取りすることで、<kbd>上矢印</kbd>や<kbd>下矢印</kbd>のキーボードイベントなどの標準入力イベントを再度有効にして、読み取りカーソルを制御します。

記事 ([`article`](/ja/docs/Web/Accessibility/ARIA/Roles/Article_Role)) ロールとは対照的に、文書 (`document`) ロールは、文書ロールを持つ他の要素との関係はなく、単にそれ含む複合ウィジェットとの関係があるだけです。 記事は関連記事を持つことができます。

### 関連する WAI-ARIA のロール、ステート、プロパティ

- `aria-expanded`
  - : 文書要素が折りたたみ可能である場合は、`true` または `false` の値を含み、文書が現在展開されているか折りたたまれているかを示します。 他の値には、文書が折りたたまれないことを意味するデフォルトの `undefined` が含まれます。
- `tabindex="0"`
  - : 支援技術のユーザーがそれにタブ移動してすぐに読み始められるように、それをフォーカス可能にするために使用します。

### キーボードインタラクション

`tabindex="0"` 属性/値のペアを設定することで、要素をフォーカス可能にするべきです。 これにより、ユーザーはそれにタブ移動でき、自動的に読み取りモードが起動し、内容をすぐに読むことができるようになります。

### 必要な JavaScript 機能

なし (任意の属性が必要とする場合を除く。 例えば、文書 (`document`) が折りたたみ可能である場合、`aria-expanded` のステートと値を維持する必要があります。)

## 例

例として、Gmail と 1 つの会話ビューがあります。 GMail はウェブアプリケーションです。 Gmail の場合、ユーザーエージェントとのやりとりのほとんどがアプリケーションによって奪われます。 ただし、会話の主題を含む 1 つの会話の開始見出しにキーボードフォーカスが設定されている場合、スクリーンリーダーのユーザーは読み取りモードのコマンドを使用してメッセージを読んだり、展開したり、折りたたんだり、操作したりできます。 \[戻る] ボタンをアクティブ化するか、関連するキーを押すことによって、フォーカスがメッセージリストに戻ると、アプリケーションとの直接やりとりモードが再び起動し、<kbd>矢印</kbd>キーを使用してリスト内の別の会話に移動できます。

## ベストプラクティス

`tabindex` 属性に値 0 を設定することにより、文書ロールを持つ項目がフォーカス可能であることを常に確認してください。 これにより、項目がタブ順序にも含まれるようになります。

### 追加の利点

文書ロールは、ユーザーがスクリーンリーダーの標準コマンドで読むべき内容であることを明確に示すことによって、支援技術の振る舞いを間接的に制御する簡単な方法です。

## 仕様書

{{Specifications}}

## スクリーンリーダーのサポート

## 関連情報

- [ARIA: widget ロール](/ja/docs/Web/Accessibility/ARIA/Roles/widget_Role)
- [ARIA: application ロール](/ja/docs/Web/Accessibility/ARIA/Roles/Application_Role)

1. [**WAI-ARIA ロール**](/ja/docs/Web/Accessibility/ARIA/Roles){{ListSubpagesForSidebar("/ja/docs/Web/Accessibility/ARIA/Roles")}}