---
title: "$ps.file.removeDirectory"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file-remove-directory
translationKey: server-script-ps-file-remove-directory
shortname: $ps.file.removeDirectory
created: 2024-12-23
updated: 2025-01-14
---

## 概要

[サーバスクリプト](../index.md)で[$ps.file](index.md)を使用して指定ディレクトリを削除します。ディレクトリ内部にサブディレクトリやファイルがあっても全て削除します。

## 前提条件

[Script.json](../../../setup/parameters/script-json.md)のDisableServerScriptFileを false に設定することが必要です。

## 構文

```
$ps.file.removeDirectory(section, path)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|section|string|○|セクション名。セクションについては[$ps.file](index.md)の「セクションについて」を参照ください。|
|path|string|○|ディレクトリ名。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|

## 戻り値

ディレクトリを削除できた場合は true、削除できなかった場合は false を返却します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、Webサーバ内の指定ディレクトリを削除します。

##### JavaScript

```
$ps.file.removeDirectory('01_develop', 'parts');
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：$ps.file](index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)

