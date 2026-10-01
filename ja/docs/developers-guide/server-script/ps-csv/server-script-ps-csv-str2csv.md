---
title: "$ps.CSV.str2csv"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-csv-str2csv
translationKey: server-script-ps-csv-str2csv
shortname: $ps.CSV.str2csv
created: 2024-12-24
updated: 2026-06-30
---

## 概要

[サーバスクリプト](../index.md)でカンマ区切り文字列を２次元配列オブジェクトに変換します。

## 制限事項

1. 変換後のカラムは全て文字列となります。数値型や日付型に変換は行いません。
2. 先頭行をヘッダとして取りあつかいません。利用者側でヘッダの有り無しを判断し必要な処理を記載してください。

## 構文

```
$ps.CSV.str2csv(text)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|text|string|○|テキスト|

## 戻り値

文字列ｘ文字列の２次元配列オブジェクト

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、文字列をcsvオブジェクトに変換してコンソールに出力しています。

##### JavaScript

```
const text = 'COLUMN01,COLUMN02,COLUMN03,COLUMN04\nA001,日本語,TRUE,2024/12/13 0:00\nA002,日本語,TRUE,2024/12/14 0:00\nA003,日本語,TRUE,2024/12/15 0:00\nA004,日本語,TRUE,2024/12/16 0:00\nA005,日本語,TRUE,2024/12/17 0:00\n';
const csv = $ps.CSV.str2csv(text);
```

##### デバッグコンソールでの操作結果

```
> csv
(6) [Array(4), Array(4), Array(4), Array(4), Array(4), Array(4)]
> csv.length
> 6
> csv[0].length
4
> csv[0].join()
'COLUMN01,COLUMN02,COLUMN03,COLUMN04'
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)

