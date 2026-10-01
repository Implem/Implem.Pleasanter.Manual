---
title: "$ps.file.getDirectoryList"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file-get-directory-list
translationKey: server-script-ps-file-get-directory-list
shortname: $ps.file.getDirectoryList
created: 2024-12-23
updated: 2025-01-14
---

## 概要

[サーバスクリプト](../index.md)で[$ps.file](index.md)を使用して指定ディレクトリ内のディレクトリ名一覧を取得します。

## 前提条件

[Script.json](../../../setup/parameters/script-json.md)のDisableServerScriptFileを false に設定することが必要です。

## 構文

```
$ps.file.getDirectoryList(section, path)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|section|string|○|セクション名。セクションについては[$ps.file](index.md)の「セクションについて」を参照ください。|
|path|string|○|ディレクトリ名。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|

## 戻り値

ディレクトリ名文字列の配列を返却します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、Webサーバ内の指定ディレクトリ内のディレクトリ名一覧を取得し、結果をログに出力します。

##### JavaScript

```
const lists  = $ps.file.getDirectoryList('test_data','parts');
context.Log('listCnt='+lists.length);
for (const element of lists) {
	context.Log('list='+element);
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：$ps.file](index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)

