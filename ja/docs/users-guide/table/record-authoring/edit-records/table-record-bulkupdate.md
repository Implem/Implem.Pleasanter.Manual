---
title: レコードの一括更新
category: テーブル機能
order: '153'
status: ''
parts: ''
urlstring: table-record-bulkupdate
translationKey: table-record-bulkupdate
shortname: 一括更新
created: 2019-10-01
updated: 2024-06-07
---

## 概要

ある項目の値をまとめて変更したいときに、一括更新機能を使用することで指定した項目の値を一括で変更することができます。

## 制限事項

1. [状況による制御](../../../hands-on/advanced/advanced-operations-process.md)にて特定の状況で項目に[読取専用](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)を設定している場合であっても、[読取専用](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)は有効になりません。  

## 前提条件

1. サイトの「更新権限」が必要です。
1. 一括更新機能を使用する場合は、エディタ画面の項目の詳細設定にて[一括更新を許可](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-bulk-update.md)というチェックボックスをオンにすることで一括更新機能が使用できるようになります。

## 操作手順

1. 一覧画面下部にある「一括更新」ボタンをクリックしてください。
![一覧画面下部の「一括更新」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/de5ff99ec2f74fdbb0c470a78fb87b88.png) 
1. 一括更新する項目、更新後の値を入力し、「一括更新」ボタンをクリックしてください。  
![更新する項目と値を指定する一括更新のダイアログ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/66020a3b96ed488ba2cef8d0c000fb5e.png)  
1. 対象レコードの[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目の値が一括更新されたことを確認してください。
![状況項目が一括更新された一覧画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/c07f26e02eca49fe968bbcc99c10373f.png)

## 関連情報

-   [応用編：プロセスと状況による制御](../../../hands-on/advanced/advanced-operations-process.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)
-   [テーブルの管理：エディタ：項目の詳細設定：一括更新を許可](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-bulk-update.md)
-   [テーブルの管理：項目：状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)