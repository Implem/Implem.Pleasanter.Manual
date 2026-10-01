---
title: 一覧表示でロックされたレコードにハイライトをつけたい
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-highlight-locked-record
translationKey: faq-highlight-locked-record
shortname: ''
created: 2020-05-22
updated: 2026-04-13
---

## 回答

[スタイル](../../developers-guide/style/index.md)を使用してください。

---

## 概要

[レコードのロック](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-record-lock.md)機能によりロック状態にあるレコードを一覧画面でハイライト表示したい場合は[スタイル](../../developers-guide/style/index.md)を設定してください。

## 事前準備

1. テーブルの管理を開きます。
1. スタイルタブを開きます。
1. 新規作成を押下し、任意のタイトルを入力し、下記のCSSを入力します。
1. 出力先を一覧とし、追加ボタンをクリックします。
1. 更新ボタンをクリックします。
1. 一覧画面でレコードがハイライトされていることを確認します。
    ![一覧画面でロックされたレコードがハイライトされている状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/4e0e241a6bd5435c9778ac09150cdad0.png)

## サンプルコード

ver1.4.20.0前後で記載方法が異なりますのでご注意ください。

#### ver1.4.20.0以降

##### CSS

```
.grid [data-locked="1"] td{ 
    background-color: pink;
}
```

#### ver1.4.19.2以前

##### CSS

```
[data-locked="1"] { 
    background-color: pink;
}
```

## 関連情報

-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブルの管理：エディタ：レコードのロックを許可](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-record-lock.md)