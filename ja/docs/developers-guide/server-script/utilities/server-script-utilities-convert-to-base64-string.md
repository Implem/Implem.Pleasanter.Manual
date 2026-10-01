---
title: utilities.ConvertToBase64String
icon: material/alpha-m-box
category: サーバスクリプト
order: '6510'
status: ''
parts: ''
urlstring: server-script-utilities-convert-to-base64-string
translationKey: server-script-utilities-convert-to-base64-string
shortname: utilities.ConvertToBase64String
created: 2022-06-03
updated: 2025-01-30
---

## 概要

「サーバースクリプト」で引数に渡した文字列をBase64形式の文字列に変換します。

## 構文

```
utilities.ConvertToBase64String(str, encoding)
```

## パラメータ

|パラメータ|型|必須|概要|
|:----------|:----------|:---:|:---------------------------|
|str|string|○|変換する文字列|
|encoding|string||[文字列のエンコーディング](https://docs.microsoft.com/ja-jp/dotnet/api/system.text.encoding?view=net-6.0)を指定（省略時には'utf-8'が指定されます。）|

## 戻り値

Base64形式文字列

## 使用例

以下の例では、文字列 "プリザンター" をBase64形式の文字列に変換してログに出力します。

##### JavaScript

```
let base64 = utilities.ConvertToBase64String('プリザンター', 'shift_jis');
context.Log(base64);
```

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.9.0 以降|機能追加|

## 関連情報

-   [文字列のエンコーディング](https://docs.microsoft.com/ja-jp/dotnet/api/system.text.encoding?view=net-6.0)
-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：スクリプト](../../../managers-guide/manage-table/scripts/index.md)