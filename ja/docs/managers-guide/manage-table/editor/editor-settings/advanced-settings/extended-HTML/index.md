---
title: 拡張HTML
category: エディタ
order: '17100'
status: ''
parts: ''
urlstring: table-management-extended-html
translationKey: table-management-extended-html
shortname: 拡張HTML
created: 2020-11-13
updated: 2026-04-27
---

## 概要

項目の詳細設定の「拡張HTML」は、[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)に配置した[項目](../../columns/index.md)の前後に、任意のHTMLを挿入する機能です。「詳細設定」画面の「拡張HTML」タブで設定します。

![項目の詳細設定画面の拡張HTMLタブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/assets/786520a7d93d499e8f5f6ada6100a2ee.png)

| 設定項目                 | 説明                                             |
| :----------------------- | :----------------------------------------------- |
| フィールドの前           | 入力したHTMLが項目の前に出力されます。           |
| ラベルの前               | 入力したHTMLが項目名の前に出力されます。         |
| ラベルとコントロールの間 | 入力したHTMLが項目名と入力欄の間に出力されます。 |
| コントロールの後         | 入力したHTMLが入力欄の後に出力されます。         |
| フィールドの後           | 入力したHTMLが項目の後に出力されます。           |

### 「拡張HTML」タブで使われている用語の意味

フィールド、ラベル、コントロールという用語の意味と、これらの前後関係は、以下の模式図のとおりです。

![フィールド、ラベル、コントロールの前後関係を示す模式図](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/assets/3187dd4c07fb42178a523bebba54ecbe.png)
/// caption
模式図
///

この模式図はHTMLのDOMツリーの構造を図示しています。  **実際の表示位置が模式図の通りになるとは限らないことに注意**してください。

## 設定例

1.  以下の設定例では、[フィールドCSS](../general/table-management-extended-field-css.md)機能を利用し、分類Aと分類Bにマージンを設定しています。このようなCSSの調整は、検証用テーブルを別途用意し、実施してください。
1.  HTMLの画面構成の仕様上、指定項目に十分な余白がない場合、「拡張HTML」で設定した内容と隣接する項目などとの予想外の重なりが起こり得ます。

### 「フィールドの前」「フィールドの後」の設定例

![フィールドの前、フィールドの後の設定例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/assets/6873484ffe894430a8089fb374a0de41.png)

```html title="フィールドの前"
<div style="clear: both; margin-left: 120px;">フィールドの前</div>
```

``` html title="フィールドの後"
<div style="clear: both; margin-left: 120px;">フィールドの後</div>
```

![「フィールドの前」「フィールドの後」を設定したときのエディタでの表示結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/assets/28953b449f3a4ed0be5d45bf1e87ecd0.png)
/// caption
エディタの表示結果
///

### 「ラベルの前」「ラベルとコントロールの間」「コントロールの後」の設定例

![ラベルの前、ラベルとコントロールの間、コントロールの後の設定例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/assets/283090b6aed242ca97e24e24a9960ebd.png)

``` html title="ラベルの前"
<div style="color:red; padding: 5px;">ラベルの前</div>
```

```html title="ラベルとコントロールの間"
<div style="clear:both; padding: 5px;">ラベルとコントロールの間</div>
```

```html title="コントロールの後"
<div style="color:red; padding: 5px;">コントロールの後</div>
```

![「ラベルの前」「ラベルとコントロールの間」「コントロールの後」を設定したときのエディタでの表示結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/assets/676054cfde424bc8a8fb5e09ae040cad.png)
/// caption
エディタでの表示結果
///

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。
1.  「拡張HTML」は「現在の設定」リストに表示される[項目](../../columns/index.md)に対して設定可能です。

## 操作手順

1.  対象のテーブルを開いてください。
1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  [テーブルの管理](../../../../index.md)をクリックしてください。
1.  [エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブをクリックしてください。
1.  [エディタの設定](../../index.md)の「現在の設定」リストから任意の項目を選択し、「詳細設定」ボタンをクリックしてください。  
1.  「拡張HTML」タブをクリックしてください。
1.  必要な設定を行い、「変更」ボタンをクリックしてください。
1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。

## 関連情報

-   [テーブル機能：レコードのエディタ画面](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：項目](../../columns/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フィールドCSS](../general/table-management-extended-field-css.md)
-   [テーブルの管理](../../../../index.md)
-   [テーブルの管理：エディタ：エディタの設定](../../index.md)
