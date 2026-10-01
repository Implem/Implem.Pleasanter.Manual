---
title: 入力必須
category: エディタ
order: '4000'
status: ''
parts: ''
urlstring: table-management-required
translationKey: table-management-required
shortname: 入力必須
created: 2021-05-01
updated: 2024-12-19
---

## 概要

[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)で「入力項目」を「必須入力」とする場合にオンにします。

## 制限事項

1.  「入力必須」は[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)、[一覧編集](../../../../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)などでユーザが値を入力する際に制限をかけることが可能ですが[インポート](../../../../../../users-guide/table/record-authoring/create-records/table-record-import.md)、[API](../../../../../../developers-guide/api/basics/api.md)などからデータを入力する際には制限されません。
1.  対象項目を「未入力」で登録したレコードが存在しても「入力必須」をオンにすることができますが、レコードの更新時に入力チェックが行われ値を入力しないと更新が行えません。
1.  [ID項目](../../columns/table-management-id.md)では設定できません。
1.  [バージョン項目](../../columns/table-management-ver.md)では設定できません。
1.  [コメント項目](../../columns/table-management-comments.md)では設定できません。
1.  「期限付きテーブル」の[完了項目](../../columns/table-management-completion-time.md)の「入力必須」はオフにできません。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 対応バージョン

| 対応バージョン | 内容                                 |
| :------------- | :----------------------------------- |
| 1.3.11.0 以降  | チェック項目の入力必須機能を追加     |
| 1.2.17.0 以降  | 添付ファイル項目の入力必須機能を追加 |

## 関連情報

-   [テーブルの管理：項目：分類](../../columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../columns/table-management-description.md)
