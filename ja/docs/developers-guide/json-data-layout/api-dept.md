---
title: Dept
category: JSONデータレイアウト
order: '10000'
status: ''
parts: ''
urlstring: api-dept
translationKey: api-dept
shortname: JSONデータレイアウト：Dept
created: 2020-02-13
updated: 2026-09-08
---

## 概要

[API](../api/basics/api.md)や[サーバスクリプト](../server-script/index.md)で[組織](../../managers-guide/department-administration/index.md)を操作する際のJSON形式のデータレイアウトです。

## データレイアウト

|項目名|プロパティ名|データ型|備考|
|:--|--|--|:--|
|テナントID|TenantId|数値|| 
|組織ID|DeptId|数値|| 
|バージョン|Ver|数値|| 
|組織コード|DeptCode|文字列|| 
|組織名|DeptName|文字列|| 
|説明|Body|文字列|| 
|コメント|Comments|文字列|| 
|作成者|Creator|数値|ユーザIDがレスポンスされます。| 
|更新者|Updator|数値|ユーザIDがレスポンスされます。| 
|作成日時|CreatedTime|文字列|| 
|更新日時|UpdatedTime|文字列|| 
|APIバージョン|ApiVersion|数値|| 
|クラスハッシュ|ClassHash|オブジェクト(文字列)|| 
|数値ハッシュ|NumHash|オブジェクト(数値)|| 
|日付ハッシュ|DateHash|オブジェクト(文字列)|| 
|説明ハッシュ|DescriptionHash|オブジェクト(文字列)||
|チェックハッシュ|CheckHash|オブジェクト(真偽値)|| 
|添付ハッシュ|AttachmentsHash|オブジェクト(文字列)|| 

## 関連情報

-   [開発者ガイド：API](../api/basics/api.md)
-   [開発者ガイド：サーバスクリプト](../server-script/index.md)
-   [組織管理機能](../../managers-guide/department-administration/index.md)