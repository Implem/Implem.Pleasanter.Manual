---
title: ごみ箱から削除
category: ユーザ管理機能
order: '150'
status: ''
parts: ''
urlstring: user-physical-delete
translationKey: user-physical-delete
shortname: ''
created: 2023-10-26
updated: 2025-07-08
---

## 概要

ユーザの削除により[ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)に格納したユーザを物理削除します。複数のユーザを一括して物理削除できます。

## 注意事項

-   この操作を行うと削除されたレコードの復元が行えません。誤って重要なデータを削除しないよう慎重に操作します。

## 事前準備

-   この操作を実行するユーザは[テナント管理者](user-management-tenant-manager.md)権限を有効にしておく必要があります。

## 操作手順

1.  「管理」メニューを開き[ユーザの管理](index.md)をクリックします。
1.  「管理」メニューを開き[ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)をクリックします。
1.  ごみ箱に格納されたユーザの一覧が表示されるので、対象のユーザを検索します。
1.  削除したいユーザをチェックします。チェック欄は各レコードの左端列です。また、全てを選択したい場合はヘッダ行のチェック欄にチェックします。
1.  「ごみ箱から削除」ボタンをクリックします。
1.  確認ダイアログが表示されるので「OK」をクリックします。
1.  画面下に「ごみ箱から〇〇件削除しました。」とメッセージが表示されます。

![ごみ箱から削除した後に表示される完了メッセージ](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/5f8e5e571fc741da8be975e41756044b.png)

## 制限事項

1.  [Deleted.json](../../setup/parameters/deleted-json.md)の「PhysicalDelete」が false の場合には「ごみ箱から削除」ボタンが非表示となり操作が行えません。

## 関連情報

-   [テーブル機能：レコードをごみ箱から削除](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)
-   [ユーザ管理機能：テナント管理者の設定](user-management-tenant-manager.md)
-   [ユーザ管理機能](index.md)
-   [パラメータ設定：Deleted.json](../../setup/parameters/deleted-json.md)
