---
title: 一覧で条件に一致した項目の文字を装飾したい
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-column-style-change
translationKey: faq-column-style-change
shortname: ''
created: 2021-08-13
updated: 2026-02-24
---

## 回答

[サーバスクリプト](../../developers-guide/server-script/index.md)と[スタイル](../../developers-guide/style/index.md)を使用してください。

---

## 概要

プリザンターの[一覧](../../managers-guide/manage-table/grid/index.md)にて、日付(日付A)が1ヶ月以内(過去含む)の場合、日付の文字色を装飾するサンプルコードです。文字の装飾は[スタイル](../../developers-guide/style/index.md)で指定します。

## 動作イメージ

![一覧画面で日付Aが1ヶ月以内のレコードの文字が装飾されている状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/530e44846774490d9dd8ee7876bf93a6.png)

## 操作手順

1. テーブルを作成してください  
1. [サーバスクリプト](../../developers-guide/server-script/index.md)を新規作成し、以下のスクリプトを記載してください。  条件には「行表示の前」をチェックして更新します。  
1. [スタイル](../../developers-guide/style/index.md)を新規作成し、以下のコードを記載してください。出力先には[一覧](../../managers-guide/manage-table/grid/index.md)をチェックして更新します。
1. [エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)から、以下のサンプルコードにあわせて、日付Aを有効化してください。
1.  [新規作成]ボタンから新しいレコードを開き、日付Aに本日の日付を入力してレコードを作成します。
1. [一覧](../../managers-guide/manage-table/grid/index.md)に戻り、日付Aが赤文字で表示されていることを確認してください。

## スクリプト

##### JavaScript

```
let now = new Date()
let limit = now.setMonth(now.getMonth() + 1);
if (model.DateA <= limit) {
   columns.DateA.ExtendedCellCss = 'alert-color';
}
```

## スタイル

ver1.4.20.0前後で記載方法が異なりますのでご注意ください。

#### ver1.4.20.0以降

##### CSS

````
.grid td.alert-color {
   color: red;
   font-weight: bold;
}
````

#### ver1.4.19.2以前

##### CSS

````
.alert-color {
   color: red;
   font-weight: bold;
}
````

## 関連情報

-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブルの管理：一覧画面](../../managers-guide/manage-table/grid/index.md)
-   [テーブル機能：レコードのエディタ画面](../../users-guide/table/record-authoring/edit-records/table-editor.md)