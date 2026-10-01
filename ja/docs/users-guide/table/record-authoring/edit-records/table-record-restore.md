---
title: レコードをごみ箱から復元
category: テーブル機能
order: '611'
status: ''
parts: ''
urlstring: table-record-restore
translationKey: table-record-restore
shortname: ごみ箱
created: 2019-04-30
updated: 2024-06-12
---

## 概要

[ごみ箱](table-record-physical-delete.md)を使用して、削除したレコードを復元します。復元は複数のレコードを一括して行えます。

## 制限事項

1. [テーブルのロック](../../../../managers-guide/manage-table/editor/allow-lock-table/index.md)が有効化されている場合には「ナビゲーションメニュー」に[ごみ箱](table-record-physical-delete.md)が表示されず操作が行えません。
1. [BinaryStorage.json](../../../../setup/parameters/binary-storage-json.md)の「Provider」が "Local" で[BinaryStorage.json](../../../../setup/parameters/binary-storage-json.md)の「RestoreLocalFiles」が false の場合、添付ファイルは復元されません。
1. [Deleted.json](../../../../setup/parameters/deleted-json.md)の「Restore」が false の場合には「復元」ボタンが非表示となり操作が行えません。

## 前提条件

1. 「サイトの管理権限」が必要です。

## 操作手順

1. 対象のテーブルに移動してください。
1. 「ナビゲーションメニュー」から「管理」→[ごみ箱](table-record-physical-delete.md)と操作してください。
1. ごみ箱に格納されたレコードの一覧が表示されるので、対象のレコードを検索してください。
1. 復元したいレコードをチェックしてください。チェック欄は各レコードの左端列です。また、全てを選択したい場合はヘッダ行のチェック欄にチェックしてください。
1. 「復元」ボタンをクリックしてください。
1. 確認ダイアログが表示されるので「OK」をクリックしてください。
1. 画面下に「〇〇件復元しました。」とメッセージが表示されたら完了です。

![ごみ箱のレコード一覧と「復元」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/b3d7f87366b74dc7acefeff388439321.png)

## 関連情報

-   [テーブル機能：レコードをごみ箱から削除](table-record-physical-delete.md)
-   [テーブルの管理：エディタ：テーブルのロックを許可](../../../../managers-guide/manage-table/editor/allow-lock-table/index.md)
-   [パラメータ設定：BinaryStorage.json](../../../../setup/parameters/binary-storage-json.md)
-   [パラメータ設定：Deleted.json](../../../../setup/parameters/deleted-json.md)