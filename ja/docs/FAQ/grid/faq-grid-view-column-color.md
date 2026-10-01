---
title: 一覧画面で特定の列の背景色を変更したい
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-grid-view-column-color
translationKey: faq-grid-view-column-color
shortname: ''
created: 2020-07-26
updated: 2026-02-24
---

## 回答

[サーバスクリプト](../../developers-guide/server-script/index.md)と[スタイル](../../developers-guide/style/index.md)を使用します。

---

## 概要

一覧画面で特定の列の背景色を変更する際は[サーバスクリプト](../../developers-guide/server-script/index.md)の[columns](../../developers-guide/server-script/columns/index.md)オブジェクトの「ExtendedCellCss」にあらかじめ[スタイル](../../developers-guide/style/index.md)で設定したスタイルを設定します。
今回は例として「開始」という名前の列の背景色を青色にします。

## 操作手順

1. 対象のテーブルを開きます。  
1. 管理→テーブルの管理をクリックします。  
1. [スタイル](../../developers-guide/style/index.md)タブを開きます。  
1. 新規作成ボタンをクリックし、ダイアログを表示します。  
1. タイトルに「背景色を青にする」等の任意のタイトルを入力、スタイルに以下のCSSを入力、出力先は一覧を設定してダイアログの変更ボタンをクリックします。
1. [サーバスクリプト](../../developers-guide/server-script/index.md)タブを開きます。
1. 新規作成ボタンをクリックし、ダイアログを表示します。  
1. タイトルに「一覧画面の数値項目の背景色を青色にする」等の任意のタイトルを入力、スクリプトに以下のCSSを入力、条件は「行表示の前」を設定してダイアログの変更ボタンをクリックします。
1. 画面下部の更新ボタンをクリックします。  
1. 対象テーブルの一覧画面を開き、開始列の背景色が青色になっていることを確認します。  

## サーバスクリプト

##### JavaScript

```
columns.NumA.ExtendedCellCss = 'blue';
```

## スタイル

ver1.4.20.0前後で記載方法が異なりますのでご注意ください。

#### ver1.4.20.0以降

##### CSS

```
.grid td.blue{
    background-color: blue;
}
```

#### ver1.4.19.2以前

##### CSS

```
.blue {
    background-color: blue;
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [開発者ガイド：サーバスクリプト：columns](../../developers-guide/server-script/columns/index.md)