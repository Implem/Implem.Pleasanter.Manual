---
title: Group
category: JSONデータレイアウト
order: '10000'
status: ''
parts: ''
urlstring: api-group
translationKey: api-group
shortname: JSONデータレイアウト：Group
created: 2020-02-13
updated: 2026-09-08
---

## 概要

[API](../api/basics/api.md)や[サーバスクリプト](../server-script/index.md)で[グループ](../../managers-guide/group-administration/index.md)を操作する際のJSON形式のデータレイアウトです。

## データレイアウト

|項目名|プロパティ名|データ型|備考|
|--|--|--|--|
|テナントID|TenantId|数値||
|グループID|GroupId|数値||
|バージョン|Ver|数値||
|グループ名|GroupName|文字列|| 
|内容|Body |文字列||
|コメント|Comments|文字列|| 
|作成者|Creator|数値|ユーザIDがレスポンスされます|
|更新者|Updator|数値|ユーザIDがレスポンスされます|
|作成日時|CreatedTime|文字列||
|更新日時|UpdatedTime|文字列||
|更新日時|UpdatedTime|文字列||
|APIバージョン|ApiVersion|数値|| 

## 関連情報

-   [開発者ガイド：API](../api/basics/api.md)
-   [開発者ガイド：サーバスクリプト](../server-script/index.md)
-   [グループ管理機能](../../managers-guide/group-administration/index.md)