---
title: 項目のラベル幅を任意の値にしたい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-label-width
translationKey: faq-label-width
shortname: ''
created: 2020-03-13
updated: 2024-04-29
---

## 回答

[スタイル](../../developers-guide/style/index.md)を使用してください。

---

## 概要

項目のラベル幅を任意の値にしたいときは[スタイル](../../developers-guide/style/index.md)をご利用ください。以下は記録テーブルにおける分類A項目のラベル幅を50pxにするサンプルです。

## 操作方法

1. 対象のテーブルを開きます。
1. ナビゲーションメニューより「管理」－[テーブルの管理](../../managers-guide/manage-table/index.md)とクリックします。
1. スタイルタブを開きます。
1. 新規作成ボタンをクリックし、ダイアログを表示します。
1. タイトルに「分類A項目のラベル幅の変更」等の任意のタイトルを入力します。
1. スタイル欄に以下のスタイルを入力します([for=～]以下の記述について、記録テーブルの際はResults_〇〇、期限付きテーブルの際はIssues_〇〇としてください）。
1. 出力先の「全て」のチェックを外し、上記のスタイルを適用したい画面にチェックします。
1. ダイアログの変更ボタンをクリックします。
1. 画面下部の更新ボタンをクリックします。
1. 対象テーブルを開き、上記のスタイルが適用されていることを確認します。

## サンプルコード

##### CSS

```
label[for="Results_ClassA"]{
   display:block;
   width:50px;
}
```

※上記は分類A項目におけるラベルの例を挙げましたが、それぞれの項目における指定方法を以下に示します。

-   分類A～分類Z→ClassA～ClassZ
-   数値A～数値Z→NumA～NumZ
-   日付A～日付Z→DateA～DateZ

（例1）記録テーブルにて、数値C項目のラベルの幅を70pxにするスタイル

##### CSS

```
label[for="Results_NumC"]{
   display:block;
   width:70px;
}
```

（例2）期限付きテーブルにて、日付B項目のラベルの幅を65pxにするスタイル

##### CSS

```
label[for="Issues_DateB"]{
   display:block;
   width:65px;
}
```

## 関連情報

-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)