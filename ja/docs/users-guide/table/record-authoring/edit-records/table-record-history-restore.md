---
title: レコードの変更履歴から復元
category: テーブル機能
order: '502'
status: ''
parts: ''
urlstring: table-record-history-restore
translationKey: table-record-history-restore
shortname: 変更履歴
created: 2021-04-17
updated: 2024-06-07
---

## 概要

[変更履歴](table-record-history-delete.md)を使用して、テーブルのレコードの変更履歴から特定バージョンの内容を復元します。この操作を行うと指定したバージョンの内容が最新バージョンとして復元され、操作前の最新バージョンの内容は変更履歴に追加されます。復元を行うとバージョンが1つ増えます。

## 制限事項

1. 本操作はレコード単位に行う必要があります。複数のレコードをまとめて操作することはできません。
1. 「[パラメータ設定：History.json](../../../../setup/parameters/history-json.md)」の「Restore」が false の場合には「復元」ボタンが非表示となり操作が行えません。

## 前提条件

1. 「読み取り権限」と「更新権限」が必要です。

## 操作手順

1. 対象のテーブルに移動してください。
1. [一覧画面](../data-analysis/table-grid.md)から対象のレコードを検索してください。
1. 対象のレコードをクリックしてください。
1. [エディタ](table-editor.md)が表示されるので「変更履歴の一覧」タブをクリックしてください。変更履歴が確認できます。
1. 復元するバージョンの行の左にあるチェックボックスをオンにして、「復元」ボタンをクリックします。
1. 「バージョン n から復元しました。」と表示されれば完了です。 n には復元元のバージョン番号が表示されます。

![「変更履歴の一覧」タブでバージョンを選び復元する画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/d6e5b837f9094677b9aac4ba90d79a42.png)

## 関連情報

-   [テーブル機能：レコードの変更履歴を削除](table-record-history-delete.md)
-   [パラメータ設定：History.json](../../../../setup/parameters/history-json.md)
-   [テーブル機能：レコードの一覧画面](../data-analysis/table-grid.md)
-   [テーブル機能：レコードのエディタ画面](table-editor.md)