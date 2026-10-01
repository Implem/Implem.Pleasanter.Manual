---
title: ごみ箱から削除
category: 組織管理機能
order: '60'
status: ''
parts: ''
urlstring: dept-physical-delete
translationKey: dept-physical-delete
shortname: ''
created: 2023-10-27
updated: 2025-07-08
---

## 概要

組織の削除により[ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)に格納した組織を物理削除します。複数の組織を一括して物理削除できます。

## 注意事項

1. この操作を行うと削除された組織の復元が行えません。誤って重要なデータを削除しないよう慎重に操作してください。

## 事前準備

- この操作を実行するユーザは[テナント管理者](../user-administration/user-management-tenant-manager.md)権限を有効にしておく必要があります。

## 操作手順

1. 「管理」メニューを開き「組織の管理」をクリックします。
1. 「管理」メニューを開き[ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)をクリックします。
1. ごみ箱に格納された組織の一覧が表示されるので、対象の組織を検索します。
1. 削除したい組織をチェックします。チェック欄は各レコードの左端列です。また、全てを選択したい場合はヘッダ行のチェック欄にチェックします。
1. 「ごみ箱から削除」ボタンをクリックします。
1. 確認ダイアログが表示されるので「OK」をクリックします。
1. 画面下に「ごみ箱から〇〇件削除しました。」とメッセージが表示されます。

![組織をごみ箱から削除した後に表示される完了メッセージ](https://pleasanter.org/files/images/ja/managers-guide/department-administration/assets/ff9da763d7164680a14714b79c248fb5.png)

## 制限事項

1. [Deleted.json](../../setup/parameters/deleted-json.md)の「Restore」が false の場合には「復元」ボタンが非表示となり操作が行えません。

## 関連情報

-   [テーブル機能：レコードをごみ箱から削除](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)
-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
-   [パラメータ設定：Deleted.json](../../setup/parameters/deleted-json.md)