---
title: レコードのロックの解除
category: テーブル機能
order: '802'
status: ''
parts: ''
urlstring: table-record-unlock
translationKey: table-record-unlock
shortname: レコードのロック
created: 2021-04-17
updated: 2024-06-07
---

## 概要

ロックされたテーブルのレコードのロックを解除します。ロックを解除するとレコードの編集や削除等の更新操作が行えるようになります。

## 前提条件

1. ロックしたユーザまたは[特権ユーザ](../../../../managers-guide/user-administration/user-management-privileged-users.md)で操作する必要があります。
1. 「読み取り権限」と「更新権限」が必要です。
1. 「ロック」項目がエディタで有効化されている必要があります。
1. 「ロック」項目の「更新権限」が必要です。

## 操作手順

1. 対象のテーブルに移動してください。
1. [一覧画面](../data-analysis/table-grid.md)から対象のレコードを検索してください。
1. 対象のレコードをクリックしてください。
1. 「ロック」項目のチェックをオフにしてください。
1. 「更新」ボタンをクリックしてください。
1. 確認メッセージが表示されますので「OK」をクリックしてください。
1. 「レコードのロックを解除しました。」と表示され、画面上部のロックされている旨の表示が消えれば完了です。

![「ロック」項目をオフにしてロックを解除する操作の画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/f26b14c832664e9a9111abd952e1262b.png)

## 関連情報

-   [ユーザ管理機能：特権ユーザの設定](../../../../managers-guide/user-administration/user-management-privileged-users.md)
-   [テーブル機能：レコードの一覧画面](../data-analysis/table-grid.md)