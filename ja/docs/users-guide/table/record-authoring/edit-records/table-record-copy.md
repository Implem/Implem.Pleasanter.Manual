---
title: レコードのコピー
category: テーブル機能
order: '701'
status: ''
parts: ''
urlstring: table-record-copy
translationKey: table-record-copy
shortname: コピー
created: 2019-06-30
updated: 2024-06-07
---

## 概要

[エディタ](table-editor.md)を使用して、テーブルのレコードをコピーします。コピーを行うとタイトルの末尾に「 - コピー」の文字列が追加されます。コピー元のレコードのIDは変更されません。コピー先のレコードは新規に作成されます。

## 制限事項

1. [添付ファイル](table-record-attachment-delete.md)はコピーできません。
1. [変更履歴](table-record-history-delete.md)はコピーできません。
1. [レコードのアクセス制御](../../../access-control/table-record-access-control.md)の設定はコピーできません。
1. 「項目の詳細設定」で[既定値でコピー](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-copy-by-default.md)がオンの項目は値がコピーされず既定値が入力されます。

## 前提条件

1. レコードの「読み取り権限」およびサイトの「作成権限」が必要です。
1. 対象[テーブル](../../index.md)で[コピーを許可](../../../../managers-guide/manage-table/editor/allow-copy/index.md)がオンになっている必要があります。

## 操作手順

1. 対象のテーブルに移動してください。
1. [一覧画面](../data-analysis/table-grid.md)から対象のレコードを検索してください。
1. 対象のレコードをクリックしてください。
1. [エディタ](table-editor.md)が表示されるので[コピー](../../../hands-on/advanced/advanced-operations-copy.md)ボタンをクリックしてください。
1. コピー設定を行うダイアログが表示されます。コピー元のレコードに記入されているコメントも含めて複製する場合は、「コメントをコピーする」にチェック。不要の場合は、チェックを外してください。
1. ダイアログの[コピー](../../../hands-on/advanced/advanced-operations-copy.md)ボタンをクリックしてください。
1. 画面下に「コピーしました。」とメッセージが表示されたら完了です。

![エディタからレコードをコピーする操作の画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/9cb3dbb087754ab1a092a8a67ebadbf9.png)

## 関連情報

-   [テーブル機能：レコードのエディタ画面](table-editor.md)
-   [テーブル機能：レコードの添付ファイルの削除](table-record-attachment-delete.md)
-   [テーブル機能：レコードの変更履歴を削除](table-record-history-delete.md)
-   [レコードのアクセス制御（レコードの編集）](../../../access-control/table-record-access-control.md)
-   [テーブルの管理：エディタ：項目の詳細設定：既定値でコピー](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-copy-by-default.md)
-   [テーブル機能](../../index.md)
-   [テーブルの管理：エディタ：コピーを許可](../../../../managers-guide/manage-table/editor/allow-copy/index.md)
-   [テーブル機能：レコードの一覧画面](../data-analysis/table-grid.md)
-   [応用編：コピーと参照コピー](../../../hands-on/advanced/advanced-operations-copy.md)