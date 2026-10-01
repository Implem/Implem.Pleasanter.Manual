---
title: 一覧画面の行の高さを調整したい
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-adjust-column-width-and-height
translationKey: faq-adjust-column-width-and-height
shortname: ''
created: 2019-09-12
updated: 2024-04-29
---

## 回答

[スタイル](../../developers-guide/style/index.md)を使用します。

---

## 概要

スタイル機能を用いて一覧画面の行高さを指定の高さに変更できます。

## 設定手順  

1. 対象のテーブルを開きます。  
1. 「管理」→[テーブルの管理](../../managers-guide/manage-table/index.md)をクリックします。  
1. [スタイル](../../developers-guide/style/index.md)タブを開きます。  
1. 「＋新規作成」ボタンをクリックし、ダイアログを表示します。   
1. タイトルに「一覧画面の行の高さを調整」等の任意のタイトルを入力します。  
1. スタイルに行の高さを調整するスタイルを入力します。  
1. 出力先の「全て」のチェックを外し、[一覧](../../managers-guide/manage-table/grid/index.md)にチェックします。  
1. ダイアログの変更ボタンをクリックします。  
1. 画面下部の更新ボタンをクリックします。  
1. 対象のテーブルの一覧画面を開き、行の高さを確認します。  

## スタイル例

行の高さを「200px」に設定するスタイルです。

##### CSS

```
.grid-row > td > * {
    max-height: 200px !important;
}
```

#### マウスオーバー時の動作について

一覧画面では項目の文字数が一定の量を超えると一定の行の高さで隠れ、マウスカーソルを対象の行にあてることで隠れている部分も表示できる仕様となっていますが、上記の指定を行うことにより行の高さが固定されます。マウスカーソルを対象の行にあてることで隠れている部分を表示するには、以下のスタイルを追加で設定してください。

##### CSS

```
.grid-row > td > *:hover {
    max-height: initial !important;
}
```

## 関連情報

-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [テーブルの管理：一覧画面](../../managers-guide/manage-table/grid/index.md)
