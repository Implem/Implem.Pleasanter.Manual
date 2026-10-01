---
title: "$ps.file.copyFile"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file-copy-file
translationKey: server-script-ps-file-copy-file
shortname: ''
created: 2025-08-01
updated: 2025-08-12
---

## 概要

[サーバスクリプト](../index.md)で[$ps.file](index.md)を使用して指定ファイルをコピーします。

## 前提条件

[Script.json](../../../setup/parameters/script-json.md)のDisableServerScriptFileを false に設定することが必要です。

## 構文

```
$ps.file.copyFile(section, sourcePath, destPath)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|section|string|○|セクション名。セクションについては[$ps.file](index.md)の「セクションについて」を参照ください。|
|sourcePath|string|○|コピー元ファイルパス。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|
|destPath|string|○|コピー先ファイルパス。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|

## 戻り値

ファイルをコピーできた場合は true、コピーできなかった場合は false を返却します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、Webサーバ内のディレクトリ "parts_01" 内の指定ファイルをディレクトリ "parts_02" にコピーします。

##### JavaScript

```
$ps.file.copyFile('01_develop', 'parts_01/document.txt', 'parts_02/document.txt');
```

以下の例では、Webサーバ内のディレクトリ "parts_01" 内の"document.txt"を同じディレクトリ内に"document_2.txt"としてコピーします。

##### JavaScript

```
$ps.file.copyFile('01_develop', 'parts_01/document.txt', 'parts_01/document_2.txt');
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.19.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：$ps.file](index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)

