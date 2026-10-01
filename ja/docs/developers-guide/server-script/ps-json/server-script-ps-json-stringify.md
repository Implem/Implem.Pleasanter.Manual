---
title: "$ps.JSON.stringify"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-json-stringify
translationKey: server-script-ps-json-stringify
shortname: $ps.JSON.stringify
created: 2024-12-24
updated: 2026-06-30
---

## 概要

[サーバスクリプト](../index.md)でmodelなどサーバスクリプトで利用可能なオブジェクトや、サーバから返却されるオブジェクトを文字列にシリアライズします。

## 構文

```
$ps.JSON.stringify(json)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|json|object|○|オブジェクト|

## 戻り値

シリアライズした文字列を返します。

## 使用例

以下の例では、jsonオブジェクトの内容をシリアライズしてコンソールに出力しています。

##### JavaScript

```
context.Log($ps.JSON.stringify({ x: 5, y: 6 }));
```

##### 出力例

```
{"x":5,"y":6}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
