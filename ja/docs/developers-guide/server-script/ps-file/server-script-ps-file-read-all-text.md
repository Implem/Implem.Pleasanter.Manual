---
title: "$ps.file.readAllText"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file-read-all-text
translationKey: server-script-ps-file-read-all-text
shortname: $ps.file.readAllText
created: 2024-12-23
updated: 2025-01-14
---

## 概要

[サーバスクリプト](../index.md)で[$ps.file](index.md)を使用してファイル読み込みをする際に使用します。ファイルの内容をすべて読み込み、文字列型で値を戻します。

## 前提条件

[Script.json](../../../setup/parameters/script-json.md)のDisableServerScriptFileを false に設定することが必要です。

## 構文

```
$ps.file.readAllText(section, path, encode=null);
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|section|string|○|セクション名。セクションについては[$ps.file](index.md)の「セクションについて」を参照ください。|
|path|string|○|ファイル名。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|
|encode|string||ファイルのエンコーディングの指定（※１）省略時は"utf-8"|

※１
System.Text.Encoding.GetEncoding のパラメータで指定できるコードページ名を指定します。

## 戻り値

ファイルの内容を文字列型で返却します。ファイルが存在しない場合はnullを返却します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、Webサーバ内のファイルを読む込み、結果をログに出力します。

##### JavaScript

```
let text = $ps.file.readAllText('01_develop', 'parts/01_parts.txt');
context.Log('text: ' + text);
```

文字コード：Shift-JIS の例
```
let text = $ps.file.readAllText('01_develop', 'parts/01_parts.txt', 'shift-jis');
context.Log('text: ' + text);
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：$ps.file](index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)

