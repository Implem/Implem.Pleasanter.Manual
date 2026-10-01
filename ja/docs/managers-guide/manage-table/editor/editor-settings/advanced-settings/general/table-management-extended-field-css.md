---
title: フィールドCSS
category: エディタ
order: '13000'
status: ''
parts: ''
urlstring: table-management-extended-field-css
translationKey: table-management-extended-field-css
shortname: フィールドCSS
created: 2020-06-30
updated: 2024-04-09
---

## 概要

「入力項目」の[表示名](table-management-label-text.md)のラベルを含む、項目のフィールド要素にCSSを適用する場合に使用します。CSSクラス名を指定することで、各項目に任意のクラス名を指定し、[スタイル](../../../../../../developers-guide/style/index.md)を適用することができます。  

## 制限事項

1.  [コメント項目](../../columns/table-management-comments.md)では使用できません。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 動作イメージ

[分類項目](../../columns/table-management-class.md)の「フィールドCSS」に「field-test」、[コントロールCSS](table-management-extended-control-css.md)に「control-test」というクラス名を指定します。

![フィールドCSSとコントロールCSSにクラス名を指定する画面（1/3）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/a69f68c0bd004d1381dadc258c31d972.png)

![フィールドCSSとコントロールCSSにクラス名を指定する画面（2/3）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/336ea80758094f04841e1df7ecb2db74.png)

![フィールドCSSとコントロールCSSにクラス名を指定する画面（3/3）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/84758c26e4564b7dbaf190d25e70d3ea.png)

指定したクラスに対して以下のようにスタイルを設定します。（ここでは新規作成にチェック）

``` css title="CSS" linenums="1"
.field-test {
      background-color: red;
}

.control-test {
     background-color: green;
}
```

新規作成で以下のように表示されます。

![指定したCSSが適用された新規作成画面（1/2）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/554eeeb9a4bc4c13928a0a7746552dea.png)

![指定したCSSが適用された新規作成画面（2/2）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/83afbf2b31334d619d01129232979723.png)

フィールドCSSではラベルの装飾、レイアウト調整、項目の表示非表示、コントロールCSSでは入力欄のサイズ変更、項目の値の取得などに使用できます。

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：表示名](table-management-label-text.md)
-   [開発者ガイド：スタイル](../../../../../../developers-guide/style/index.md)
-   [テーブルの管理：項目：コメント](../../columns/table-management-comments.md)
-   [テーブルの管理：項目：分類](../../columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロールCSS](table-management-extended-control-css.md)
