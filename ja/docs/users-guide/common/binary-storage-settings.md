---
title: ファイルの保存先指定
category: 共通機能
order: '0'
status: ''
parts: ''
urlstring: binary-storage-settings
translationKey: binary-storage-settings
shortname: 共通機能：ファイルの保存先指定
created: 2026-08-04
updated: 2026-08-12
---

## 概要

-   アイコンファイル  
-   「[内容](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)」項目、「説明」項目、[コメント](comment.md)へ貼り付けた画像ファイル  
-   添付ファイル

上記ファイルの保存先は、以下の3つから選択できます。

1. ローカル
1. データベース
1. Azure Blob Storage

ファイルの保存先を設定するには[BinaryStorage.json](../../setup/parameters/binary-storage-json.md)を編集してください。ファイル保存先ごとに最低限設定が必要なパラメータは以下の通りです。

|保存先|設定が必要なパラメータ|
|:--|:--|
|データベース|Provider|
|ローカル|Provider<br>Path|
|Azure Blob Storage|Provider<br>AzureBlobStorageAccountUri<br>AzureBlobContainerName|

## 対応バージョン

|対応バージョン|内容|
|---|---|
|1.5.7.0 以降|Azure Blob Storageを追加|

## 関連情報

-   [共通機能：コメントを追加](comment.md)

