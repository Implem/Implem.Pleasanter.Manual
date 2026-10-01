---
title: hidden.Add
icon: material/alpha-m-box
category: サーバスクリプト
order: '60010'
status: ''
parts: ''
urlstring: server-script-hidden-add
translationKey: server-script-hidden-add
shortname: hidden.Add
created: 2021-10-19
updated: 2023-08-22
---

## 概要

[サーバスクリプト](../index.md)でHTMLのhiddenに新しい要素を追加します。

## 構文

```
hidden.Add(key, value);
```

## パラメータ

|No|パラメータ|型|必須|概要|
|:--|:----------|:----------|:---:|:---------------------------|
|1|key|string|○|hidden要素のid|
|2|value|object|○|hidden要素のvalue|

## 戻り値

戻り値はありません。

## 使用例

以下の例では、自身が所属するグループのIDの配列をJSONに変換して、hidden要素（ID:MyGroups）に出力します。

##### JavaScript

```
hidden.Add('MyGroups', JSON.stringify(Array.from(context.Groups)));
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)