---
title: レコードの変更履歴を削除
category: テーブル機能
order: '503'
status: ''
parts: ''
urlstring: table-record-history-delete
translationKey: table-record-history-delete
shortname: 変更履歴
created: 2021-04-17
updated: 2024-06-07
---

## 概要

「変更履歴」を使用して、テーブルのレコードの変更履歴から特定バージョンの内容を削除します。複数のバージョンをまとめて削除できます。

## 注意事項

1. この操作を行うと削除されたバージョンの復元が行えません。誤って重要なデータを削除しないよう慎重に操作してください。

## 制限事項

1. 最新バージョンを削除することはできません。
1. 「[パラメータ設定：History.json](../../../../setup/parameters/history-json.md)」の「PhysicalDelete」が false の場合には「変更履歴を削除」ボタンが非表示となり操作が行えません。

## 前提条件

1. 「サイトの管理権限」が必要です。

## 操作手順

1. 対象のテーブルに移動してください。
1. [一覧画面](../data-analysis/table-grid.md)から対象のレコードを検索してください。
1. 対象のレコードをクリックしてください。
1. [エディタ](table-editor.md)が表示されるので「変更履歴の一覧」タブをクリックしてください。変更履歴が確認できます。
1. 削除するバージョンの行の左にあるチェックボックスをオンにして、「変更履歴を削除」ボタンをクリックします。複数のバージョンを同時にチェックすることができます。
1. 「履歴を n 件削除しました。」と表示されれば完了です。 n には削除した履歴の件数が表示されます。

![「変更履歴の一覧」タブでバージョンを選び履歴を削除する画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/5ddf0c7b1468402d976384189d385ea5.png)

## 関連情報

-   [パラメータ設定：History.json](../../../../setup/parameters/history-json.md)
-   [テーブル機能：レコードの一覧画面](../data-analysis/table-grid.md)
-   [テーブル機能：レコードのエディタ画面](table-editor.md)