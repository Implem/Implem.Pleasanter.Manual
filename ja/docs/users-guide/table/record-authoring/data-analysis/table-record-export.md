---
title: レコードのエクスポート
category: テーブル機能
order: '231'
status: ''
parts: ''
urlstring: table-record-export
translationKey: table-record-export
shortname: エクスポート
created: 2019-04-29
updated: 2026-07-14
---

## 概要

テーブルに格納されている個々のレコードまたはすべてのレコードをCSVファイルとして書き出せます。

#### エクスポート時の書式を設定する

エクスポートする項目の順序などの設定は[エクスポートの書式設定](../../../../managers-guide/manage-table/export/index.md)で行えます。エクスポートの書式設定には管理者権限が必要です。

## 制限事項

1. 「子テーブル」の項目を一覧画面に表示している場合には、一覧画面の左端に表示されるレコード選択のチェックボックスは表示されません。
1. 「更新権限」、「削除権限」、「エクスポート権限」のいずれも持たない場合は、一覧画面の左端に表示されるレコード選択のチェックボックスは表示されません。

## 前提条件

1. [テーブル](../../index.md)の「エクスポート権限」が必要です。

## 操作手順

レコードを指定した書式でエクスポートできます。

1. [一覧](../../../../managers-guide/manage-table/grid/index.md)画面左端のチェックボックスで、エクスポートしたいレコードを選択してください。レコードを1つも選択しない場合には、すべてのレコードがエクスポートされます。
1.  コマンドボタンエリアの[エクスポート](../../../../developers-guide/api/table-operations/api-export.md)ボタンをクリックしてください。[エクスポート](../../../../developers-guide/api/table-operations/api-export.md)ボタンが表示されない場合は、管理者に相談してください。
1. [書式](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-format.md)を選択してください。
1. 「文字コード」を選択してください。
1. [エクスポート](../../../../developers-guide/api/table-operations/api-export.md)ボタンをクリックしてください。
1. ファイルがダウンロードされるか、ダウンロードURLが記載されたメールが届きます。

## コメントをJSON形式でエクスポートする

エクスポート時の書式として「標準」書式を選択すると、「コメントをJSON形式でエクスポートする」チェックボックスが表示されます。

![「コメントをJSON形式でエクスポートする」があるエクスポートのダイアログ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-analysis/assets/83ada5f5901b40c58673267427ffbc45.png)

必要な場合は有効化してください。

## 関連情報

-   [テーブルの管理：エクスポート](../../../../managers-guide/manage-table/export/index.md)
-   [テーブル機能](../../index.md)
-   [テーブルの管理：一覧画面](../../../../managers-guide/manage-table/grid/index.md)
-   [開発者ガイド：API：テーブル操作：テーブルのエクスポート](../../../../developers-guide/api/table-operations/api-export.md)
-   [テーブルの管理：エディタ：項目の詳細設定：書式](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-format.md)