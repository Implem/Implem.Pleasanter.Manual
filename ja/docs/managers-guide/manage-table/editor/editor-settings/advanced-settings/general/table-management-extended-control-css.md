---
title: コントロールCSS
category: エディタ
order: '13500'
status: ''
parts: ''
urlstring: table-management-extended-control-css
translationKey: table-management-extended-control-css
shortname: コントロールCSS
created: 2021-05-03
updated: 2024-04-09
---

## 概要

「入力項目」の[表示名](table-management-label-text.md)のラベルを除く、項目のインプット要素にCSSを適用する場合に使用します。CSSクラス名を指定することで、各項目に任意のクラス名を指定し、[スタイル](../../../../../../developers-guide/style/index.md)を適用することができます。  

## 制限事項

1.  [コメント項目](../../columns/table-management-comments.md)では使用できません。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 動作イメージ

[分類項目](../../columns/table-management-class.md)の[フィールドCSS](table-management-extended-field-css.md)に「field-test」、「コントロールCSS」に「control-test」というクラス名を指定します。

![フィールドCSSとコントロールCSSにクラス名を指定する画面（1/3）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/40320be076d84becb5f7e077a25f02cb.png)

![フィールドCSSとコントロールCSSにクラス名を指定する画面（2/3）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/094894fae43f4ba0b2b10096b3d9c46d.png)

![フィールドCSSとコントロールCSSにクラス名を指定する画面（3/3）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/1896b78572494a169e3766e0088e271e.png)

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

![指定したCSSが適用された新規作成画面（1/2）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/8a9fe308d3a74b2295db40638710bafa.png)

![指定したCSSが適用された新規作成画面（2/2）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/fa1d84b47f4b4d0f8d158dd1ed39d282.png)

フィールドCSSではラベルの装飾、レイアウト調整、項目の表示非表示、コントロールCSSでは入力欄のサイズ変更、項目の値の取得などに使用できます。

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：表示名](table-management-label-text.md)
-   [開発者ガイド：スタイル](../../../../../../developers-guide/style/index.md)
-   [テーブルの管理：項目：コメント](../../columns/table-management-comments.md)
-   [テーブルの管理：項目：分類](../../columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フィールドCSS](table-management-extended-field-css.md)
