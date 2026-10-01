---
title: context.ResponseSet
icon: material/alpha-m-box
category: サーバスクリプト
order: '2000'
status: ''
parts: ''
urlstring: server-script-context-response-set
translationKey: server-script-context-response-set
shortname: context.ResponseSet
created: 2023-04-04
updated: 2023-06-21
---

## 概要

[サーバスクリプト](../index.md)でフォームに情報を格納します。`context.Addresponse`のmethodパラメータに`'Set'`を指定した場合と同じ動作をします。

## 構文

``` javascript
context.ResponseSet(target,value)
```

## パラメータ

|パラメータ|型|概要|
|:--|:--|:--|
|target|string|対象の要素のIDを指定します。|
|value|object|要素や値を指定します。|

## 戻り値

戻り値はありません。

## 使用例

以下の例では、フォーム（`$p.data.MainForm`）に以下の情報を格納します。

格納する情報

|項目|値|
|:--|:--|
|数値A項目|123|

``` javascript linenums="1"
context.ResponseSet('NumA',123);
// 以下と同じ動作をします。
// context.AddResponse('Set', 'NumA',123);
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
