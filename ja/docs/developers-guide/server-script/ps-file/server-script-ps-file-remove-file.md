---
title: "$ps.file.removeFile"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file-remove-file
translationKey: server-script-ps-file-remove-file
shortname: $ps.file.removeFile
created: 2024-12-23
updated: 2025-01-14
---

## 概要

[サーバスクリプト](../index.md)で[$ps.file](index.md)を使用して指定ファイルの削除を行います。

## 前提条件

[Script.json](../../../setup/parameters/script-json.md)のDisableServerScriptFileを false に設定することが必要です。

## 構文

```
$ps.file.removeFile(section, path)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|section|string|○|セクション名。セクションについては[$ps.file](index.md)の「セクションについて」を参照ください。|
|path|string|○|ファイル名。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|

## 戻り値

ファイルを削除できた場合は true、削除できなかった場合は false を返却します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、Webサーバ内の指定ファイルの削除を行います。

##### JavaScript

```
$ps.file.removeFile('01_develop', 'parts/01_parts.txt');
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：$ps.file](index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)

