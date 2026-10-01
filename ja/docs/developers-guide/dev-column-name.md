---
title: 項目名とデータベース上のカラム名の対応
category: 開発者ガイド
order: '0'
status: ''
parts: ''
urlstring: dev-column-name
translationKey: dev-column-name
shortname: カラム名,データベースのカラム名
created: 2020-01-27
updated: 2024-12-19
---

## 概要

プリザンターの項目名とデータベース上のカラム名の対応について説明します。データベースのカラム名は[API](api/basics/api.md)でパラメータを指定する場合、[スクリプト](../managers-guide/manage-table/scripts/index.md)、[サーバスクリプト](server-script/index.md)、[ルックアップ](../users-guide/hands-on/advanced/advanced-operations-link.md)等で[項目](../managers-guide/manage-table/editor/editor-settings/columns/index.md)を指定するときに利用してください。

## 対応表

|項目名|項目カテゴリ|カラム名|データタイプ|期限付きテーブル|記録テーブル|
|:--|:--|:--|:--|:--|:--|
|サイトId|基本|SiteId|数値|〇|〇|
|レコードId|基本|期限付きテーブルの場合はIssueId、記録テーブルの場合はResultId|数値|〇|〇|
|バージョン|基本|Ver|数値|〇|〇|
|タイトル|基本|Title|文字列|〇|〇|
|内容|基本|Body|文字列|〇|〇|
|開始|基本|StartTime|日時|〇|×|
|完了|基本|CompletionTime|日時|〇|×|
|作業量|基本|WorkValue|数値|〇|×|
|進捗率|基本|ProgressRate|数値|〇|×|
|残作業量|基本|RemainingWorkValue|数値|〇|×|
|状況|基本|Status|数値|〇|〇|
|管理者|基本|Manager|数値|〇|〇|
|担当者|基本|Owner|数値|〇|〇|
|ロック|基本|Locked|論理値|〇|〇|
|コメント|基本|Comments|文字列|〇|〇|
|作成者|基本|Creator|数値|〇|〇|
|更新者|基本|Updator|数値|〇|〇|
|作成日時|基本|CreatedTime|日時|〇|〇|
|更新日時|基本|UpdatedTime|日時|〇|〇|
|分類A～分類Z|分類|ClassA～ClassZ|文字列|〇|〇|
|数値A～数値Z|数値|NumA～NumZ|数値|〇|〇|
|日付A～日付Z|日付|DateA～DateZ|日時|〇|〇|
|説明A～説明Z|説明|DescriptionA～DescriptionZ|文字列|〇|〇|
|チェックA～チェックZ|チェック|CheckA～CheckZ|論理値|〇|〇|
|添付ファイルA～添付ファイルZ|添付ファイル|AttachmentsA～AttachmentsZ|文字列|〇|〇|

## 関連情報

-   [開発者ガイド：API](api/basics/api.md)
-   [テーブルの管理：スクリプト](../managers-guide/manage-table/scripts/index.md)
-   [開発者ガイド：サーバスクリプト](server-script/index.md)
-   [応用編：リンク](../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：項目](../managers-guide/manage-table/editor/editor-settings/columns/index.md)