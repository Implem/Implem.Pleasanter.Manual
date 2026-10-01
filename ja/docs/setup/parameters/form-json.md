---
title: Form.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: form-json
translationKey: form-json
shortname: Form.json
created: 2025-11-28
updated: 2025-12-09
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Enabled|false|[フォーム](../../managers-guide/manage-table/form/index.md)機能の有効化/無効化をtrue/falseで指定します。|
|AttachmentExcludedExtensions| [".exe", ".dll", ".com"]| [添付ファイル](../../users-guide/table/record-authoring/edit-records/table-record-attachment-delete.md)項目で添付不可とする拡張子のリストを指定します。たとえば、拡張子[".exe"]を指定した場合、attachment.exe.zipのように拡張子を重ねたファイルも、添付不可となります。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.23.0 以降|Form.jsonを追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [テーブルの管理：フォーム](../../managers-guide/manage-table/form/index.md)
-   [テーブル機能：レコードの添付ファイルの削除](../../users-guide/table/record-authoring/edit-records/table-record-attachment-delete.md)
