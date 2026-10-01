---
title: "$ps.JSON.parse"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-json-parse
translationKey: server-script-ps-json-parse
shortname: $ps.JSON.parse
created: 2024-12-24
updated: 2025-01-14
---

## 概要

[サーバスクリプト](../index.md)でシリアライズしたjson文字列をサーバスクリプトで利用可能なオブジェクトにデシリアライズします。

## 構文

```
$ps.JSON.parse(text)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|text|string|○|json文字列|

## 戻り値

デシリアライズしたオブジェクトを返します。

## 使用例

以下の例では、json文字列をjsonオブジェクトにデシリアライズしてコンソールに出力しています。

##### JavaScript

```
const json = $ps.JSON.parse('{ "x": 5, "y": 6 }');
context.Log(`json.x=${json.x}`);
context.Log(`json.y=${json.y}`);
```

##### 出力例

```
json.x=5
json.y=6
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
