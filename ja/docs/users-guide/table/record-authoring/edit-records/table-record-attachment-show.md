---
title: レコードの添付ファイルの表示
category: テーブル機能
order: '904'
status: ''
parts: ''
urlstring: table-record-attachment-show
translationKey: table-record-attachment-show
shortname: 添付ファイル,ファイル表示,05.レコード作成,プレビュー表示
created: 2024-09-04
updated: 2025-10-24
---

## 概要

[テーブル](../../index.md)の「レコード」に添付された[添付ファイル](table-record-attachment-delete.md)をブラウザで参照する機能です。ご利用のブラウザで表示可能なファイルの場合は別タブでプレビュー表示します。表示不可能なファイルの場合はダウンロードします。

## 制限事項

1. 添付ファイルのプレビュー表示は、ご利用のブラウザが対応する一部のファイル形式に限定されます。
1. プレビュー表示できないファイルの場合は[ダウンロード](table-record-attachment-download.md)します。その際、ファイル名は「show」となります。

## 前提条件

1. サイトまたはレコードの「読み取り権限」が必要です。
1. [添付ファイル](table-record-attachment-delete.md)項目の「読み取り権限」が必要です。
1. プレビュー表示は別タブで表示します（ver1.4.8以降）。ver1.4.7以前は同一タブで表示します。

## 操作手順

1. 対象のテーブルに移動してください。
1. [一覧画面](../data-analysis/table-grid.md)から対象のレコードを検索してください。
1. 対象のレコードをクリックしてください。
1. 添付ファイル欄から対象のファイルの左端の虫眼鏡アイコンをクリックしてください。  
    ※ファイル名をクリックすると[ダウンロード](table-record-attachment-download.md)になります。
1. 別タブでプレビュー表示します。

![添付ファイル欄の虫眼鏡アイコンからプレビュー表示する様子](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/11e2be083c894dc7b4f6dab4853262f7.png)

### 表示可能なファイル種類

プレビュー表示可能なファイル種類は[BinaryStorage.json](../../../../setup/parameters/binary-storage-json.md)のBrowserAllowMimeTypesにMIMEタイプを指定することで設定できます。既定では以下のファイルがプレビュー表示できるように設定されています。

1. PDFファイル
1. 画像ファイル（.png、.jpg、.gif）
1. テキストファイル（.txt）

※テキストファイルは文字コードによって文字化けして表示する場合があります。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.21.0以降|表示可能なファイル種類をBinaryStorage.jsonのBrowserAllowMimeTypesで制御するように変更|
|1.4.8.0以降|別タブでプレビュー表示するように変更|

## 関連情報

-   [テーブル機能](../../index.md)
-   [テーブル機能：レコードの添付ファイルの削除](table-record-attachment-delete.md)
-   [テーブル機能：レコードの添付ファイルのダウンロード](table-record-attachment-download.md)
-   [テーブル機能：レコードの一覧画面](../data-analysis/table-grid.md)
-   [パラメータ設定：BinaryStorage.json](../../../../setup/parameters/binary-storage-json.md)