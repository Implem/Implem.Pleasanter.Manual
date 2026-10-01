---
title: レコードの参照コピー
category: テーブル機能
order: '702'
status: ''
parts: ''
urlstring: table-record-referencecopy
translationKey: table-record-referencecopy
shortname: 参照コピー
created: 2023-06-22
updated: 2025-07-24
---

## 概要

[エディタ](table-editor.md)を使用して、テーブルのレコードを参照コピーします。参照コピーを行うとコピー元のレコード内容がすべて記入された状態で新規作成画面が開きます。

## 制限事項

1. [添付ファイル](table-record-attachment-delete.md)はコピーできません。
1. [変更履歴](table-record-history-delete.md)はコピーできません。
1. [レコードのアクセス制御](../../../access-control/table-record-access-control.md)の設定はコピーできません。
1. 「項目の詳細設定」で[既定値でコピー](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-copy-by-default.md)がオンの項目は値がコピーされず既定値が入力されます。
1. [コメント](../../../common/comment.md)はコピーできません。

## 前提条件

1. レコードの「読み取り権限」およびサイトの「作成権限」が必要です。
1. 対象[テーブル](../../index.md)で[参照コピーを許可](../../../../managers-guide/manage-table/editor/allow-reference-copy/index.md)がオンになっている必要があります。

## 操作手順

1. 対象のテーブルに移動してください。
1. [一覧画面](../data-analysis/table-grid.md)から対象のレコードを検索してください。
1. 対象のレコードをクリックしてください。
1. [エディタ](table-editor.md)が表示されるので[参照コピー](../../../hands-on/advanced/advanced-operations-copy.md)ボタンをクリックしてください。
1. コピー元のレコード内容がすべて記入された状態で新規作成画面が開きます。

![参照コピーでコピー元の内容が入力された新規作成画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/cdbac824b28843a28380ceda4c765421.png)

## 関連情報

-   [テーブル機能：レコードのエディタ画面](table-editor.md)
-   [テーブル機能：レコードの添付ファイルの削除](table-record-attachment-delete.md)
-   [テーブル機能：レコードの変更履歴を削除](table-record-history-delete.md)
-   [レコードのアクセス制御（レコードの編集）](../../../access-control/table-record-access-control.md)
-   [テーブルの管理：エディタ：項目の詳細設定：既定値でコピー](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-copy-by-default.md)
-   [共通機能：コメントを追加](../../../common/comment.md)
-   [テーブル機能](../../index.md)
-   [テーブルの管理：エディタ：参照コピーを許可](../../../../managers-guide/manage-table/editor/allow-reference-copy/index.md)
-   [テーブル機能：レコードの一覧画面](../data-analysis/table-grid.md)
-   [応用編：コピーと参照コピー](../../../hands-on/advanced/advanced-operations-copy.md)