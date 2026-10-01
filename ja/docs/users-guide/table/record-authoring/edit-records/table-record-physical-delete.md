---
title: レコードをごみ箱から削除
category: テーブル機能
order: '612'
status: ''
parts: ''
urlstring: table-record-physical-delete
translationKey: table-record-physical-delete
shortname: ごみ箱
created: 2021-04-17
updated: 2024-06-12
---

## 概要

レコードの削除により「ごみ箱」に格納されたレコードを削除します。削除は複数のレコードを一括して行えます。

## 注意事項

1. この操作を行うと削除されたレコードの復元が行えません。誤って重要なデータを削除しないよう慎重に操作してください。

## 制限事項

1. テーブルがロックされている場合には「ナビゲーションメニュー」に「ごみ箱」が表示されず操作が行えません。
1. 「[パラメータ設定：Deleted.json](../../../../setup/parameters/deleted-json.md)」の「PhysicalDelete」が false の場合には「ごみ箱から削除」ボタンが非表示となり操作が行えません。

## 前提条件

1. 「サイトの管理権限」が必要です。

## 操作手順

1. 対象のテーブルに移動してください。
1. 「ナビゲーションメニュー」から「管理」→「ごみ箱」と操作してください。
1. ごみ箱に格納されたレコードの一覧が表示されるので、対象のレコードを検索してください。
1. 削除したいレコードをチェックしてください。チェック欄は各レコードの左端列です。また、全てを選択したい場合はヘッダ行のチェック欄にチェックしてください。
1. 「ごみ箱から削除」ボタンをクリックしてください。
1. 確認ダイアログが表示されるので「OK」をクリックしてください。
1. 画面下に「ごみ箱から〇〇件削除しました。」とメッセージが表示されたら完了です。

![ごみ箱のレコード一覧と「ごみ箱から削除」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/d3fec15bf9be4a35adeb8da0101b99f9.png)

## 関連情報

-   [パラメータ設定：Deleted.json](../../../../setup/parameters/deleted-json.md)