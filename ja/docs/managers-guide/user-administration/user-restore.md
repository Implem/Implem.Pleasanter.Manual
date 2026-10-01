---
title: ごみ箱から復元
category: ユーザ管理機能
order: '140'
status: ''
parts: ''
urlstring: user-restore
translationKey: user-restore
shortname: ''
created: 2023-10-26
updated: 2025-07-08
---

## 概要

[ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)から、削除したユーザを復元します。復元は複数のユーザを一括して行えます。

## 事前準備

-   この操作を実行するユーザは[テナント管理者](user-management-tenant-manager.md)権限を有効にしておく必要があります。

## 操作手順

1.  「管理」メニューを開き[ユーザの管理](index.md)をクリックします。
1.  「管理」メニューを開き[ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)をクリックします。
1.  ごみ箱に格納されたユーザの一覧が表示されるので、対象のユーザを検索します。
1.  復元したいユーザをチェックします。チェック欄は各レコードの左端列です。また、全てを選択したい場合はヘッダ行のチェック欄にチェックします。
1.  「復元」ボタンをクリックします。
1.  確認ダイアログが表示されるので「OK」をクリックします。
1.  画面下に「〇〇件復元しました。」とメッセージが表示されます。

![ごみ箱から復元した後に表示される完了メッセージ](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/4939ee9e177d47d4a63ea8943cec880f.png)

## 制限事項

1.  [Deleted.json](../../setup/parameters/deleted-json.md)の「Restore」が false の場合には「復元」ボタンが非表示となり操作が行えません。

## 関連情報

-   [テーブル機能：レコードをごみ箱から削除](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)
-   [ユーザ管理機能：テナント管理者の設定](user-management-tenant-manager.md)
-   [ユーザ管理機能](index.md)
-   [パラメータ設定：Deleted.json](../../setup/parameters/deleted-json.md)
