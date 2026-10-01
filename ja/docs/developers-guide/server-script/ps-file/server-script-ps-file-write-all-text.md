---
title: "$ps.file.writeAllText"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file-write-all-text
translationKey: server-script-ps-file-write-all-text
shortname: $ps.file.writeAllText
created: 2024-12-23
updated: 2025-01-14
---

## 概要

[サーバスクリプト](../index.md)で[$ps.file](index.md)を使用してファイル書き込みをする際に使用します。引数で渡した文字列を全てファイルに保存します。同名のファイルがあった場合には上書き更新します。同名のファイルがない場合にはファイルを新規作成します。

## 構文

```
$ps.file.writeAllText(section, path, data, encode=null)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|section|string|○|セクション名。セクションについては[$ps.file](index.md)の「セクションについて」を参照ください。|
|path|string|○|ファイル名。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|
|data|string|○|出力する文字列|
|encode|string||ファイルのエンコーディングの指定（※１）省略時は"utf-8"|

※１
.NETライブラリのSystem.Text.Encoding.GetEncoding のパラメータで指定できるコードページ名を指定します。

## 戻り値

ファイルを出力できた場合は true、出力できなかった場合は false を返却します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、Webサーバ内に指定したファイル名でファイルを書き込みます。

##### JavaScript

```
$ps.file.writeAllText('01_develop', 'parts/01_parts.txt', 'write data');
```

文字コード：Shift-JIS の例
```
$ps.file.writeAllText('01_develop', 'parts/01_parts.txt', 'write data','shift-jis');
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：$ps.file](index.md)

