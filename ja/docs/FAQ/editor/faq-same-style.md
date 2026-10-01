---
title: 複数の項目に同じスタイルを適用したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-same-style
translationKey: faq-same-style
shortname: ''
created: 2020-07-31
updated: 2024-04-29
---

## 回答

[フィールドCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-field-css.md)、[コントロールCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-control-css.md)機能を使用してください。

---

## 概要

複数の項目に同じスタイルを適用する際、それぞれの項目のセレクタに対して個別にCSSを適用することもできますが、[フィールドCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-field-css.md)、[コントロールCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-control-css.md)機能を用いると1つのclassセレクタで同内容を設定できます。

## 操作方法

以下は編集画面にて分類A、数値A、日付A項目の背景色を黄色に変更する設定方法です。

1.  対象のテーブルを開きます。
1.  管理→テーブルの管理をクリックします。
1.  エディタタブを選択します。
1.  現在の設定から分類A項目を選択し、詳細設定ボタンをクリックします。
1.  [フィールドCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-field-css.md)、[コントロールCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-control-css.md)へ任意の名前を入力します。[^1]
1.  手順4.と手順5.の操作を数値A、日付A項目にも行います。
1.  [スタイル](../../developers-guide/style/index.md)タブを開きます。
1.  新規作成ボタンをクリックし、ダイアログを表示します。
1.  タイトルに「分類A, 数値A, 日付A項目の背景色を黄色にする」等の任意のタイトルを入力します。
1.  スタイル欄に以下のスタイルを入力します。

``` css title="CSS" linenums="1"
.color-yellow input{
    background-color:yellow;
}
```

1.  出力先の「全て」のチェックを外し、「編集」のみにチェックを入れます。
1.  ダイアログの変更ボタンをクリックします。
1.  画面下部の更新ボタンをクリックします。
1.  対象テーブルの編集画面などを確認し、分類A, 数値A, 日付Aの項目背景が黄色になっていることを確認します。

[^1]: 今回は例として「color-yellow」と入力します。複数のクラスを設定したい場合は、以下のように半角スペースで区切って入力してください。  
（例）`color-yellow textcolor-red`

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：フィールドCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロールCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-control-css.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
