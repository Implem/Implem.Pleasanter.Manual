---
title: context.Redirect
icon: material/alpha-m-box
category: サーバスクリプト
order: '2000'
status: ''
parts: ''
urlstring: server-script-context-redirect
translationKey: server-script-context-redirect
shortname: context.Redirect
created: 2022-07-19
updated: 2025-01-30
---

## 概要

[サーバスクリプト](../index.md)でブラウザにページ遷移を実行させます。

## 制限事項

1. 「画面表示の前」の[条件](../../../FAQ/editor/faq-condition-mode-range.md)のみ使用できます。

## 構文

``` javascript
context.Redirect(url);
```

## パラメータ

|パラメータ|型|必須|概要|
|:----------|:----------|:---:|:---------------------------|
|url|string|○|URL|

## 戻り値

戻り値はありません。

## 使用例

下記の例のサーバスクリプトが実行されるとブラウザが指定のページに遷移します。

##### JavaScript

``` javascript
context.Redirect('http://www.example.com/');
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.13.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
