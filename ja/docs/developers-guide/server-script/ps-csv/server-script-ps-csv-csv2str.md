---
title: "$ps.CSV.csv2str"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-csv-csv2str
translationKey: server-script-ps-csv-csv2str
shortname: $ps.CSV.csv2str
created: 2024-12-24
updated: 2026-06-30
---

## 概要

[サーバスクリプト](../index.md)で２次元配列オブジェクトを文字列に変換します。

## 構文

```
$ps.CSV.csv2str(csv)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|csv|object|○|オブジェクト|

## 戻り値

カンマ区切り文字列に変換したものを返却します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、２次元配列オブジェクトを文字列に変換してコンソールに出力しています。

##### JavaScript

```
const csv  = [
  ['label', 'nnum1', 'num2'], 
  ['a', '1', '3'], 
  ['b', '2', '4'], 
];
const text = $ps.CSV.csv2str(csv);
context.Log(text);
```

##### 出力例

```
label,nnum1,num2
a,1,3
b,2,4
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)

