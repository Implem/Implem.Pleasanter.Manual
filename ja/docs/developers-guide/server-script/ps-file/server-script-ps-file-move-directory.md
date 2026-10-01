---
title: "$ps.file.moveDirectory"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file-move-directory
translationKey: server-script-ps-file-move-directory
shortname: $ps.file.moveDirectory
created: 2024-12-23
updated: 2025-01-14
---

## 概要

[サーバスクリプト](../index.md)で[$ps.file](index.md)を指定ディレクトリの名称変更または移動を行います。

## 前提条件

[Script.json](../../../setup/parameters/script-json.md)のDisableServerScriptFileを false に設定することが必要です。

## 構文

```
$ps.file.moveDirectory(section, old_name, new_name)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|section|string|○|セクション名。セクションについては[$ps.file](index.md)の「セクションについて」を参照ください。|
|old_name|string|○|旧ディレクトリ名。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|
|new_name|string|○|新ディレクトリ名。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|

## 戻り値

ディレクトリを移動できた場合は true、移動できなかった場合は false を返却します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、Webサーバ内の指定ディレクトリ名を変更します。

##### JavaScript

```
$ps.file.moveDirectory('01_develop', 'parts', 'parts_old');
```

以下の例では、Webサーバ内の指定ディレクトリを移動します。

##### JavaScript

```
$ps.file.moveDirectory('01_develop','parts/01_parts', 'parts_old/01_parts');
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：$ps.file](index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)

