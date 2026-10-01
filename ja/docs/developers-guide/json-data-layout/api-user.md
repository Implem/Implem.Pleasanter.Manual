---
title: User
category: JSONデータレイアウト
order: '10000'
status: ''
parts: ''
urlstring: api-user
translationKey: api-user
shortname: JSONデータレイアウト：User
created: 2020-02-13
updated: 2023-01-05
---

## 概要

[API](../api/basics/api.md)や[サーバスクリプト](../server-script/index.md)で[ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)を操作する際のJSON形式のデータレイアウトです。

## データレイアウト

|項目名|プロパティ名|データ型|備考|
|:--|--|--|:--|
|テナントID|TenatId|数値|| 
|ユーザID|UserId|数値|| 
|バージョン|Ver|数値|| 
|ログインID|LoginId|文字列|| 
|グローバルID|GlobalId|文字列|| 
|ユーザ名|Name|文字列|| 
|ユーザコード|UserCode|文字列|| 
|名|LastName|文字列|| 
|姓|FirstName|文字列|| 
|生年月日|Birthday|文字列|| 
|性別|Gender|文字列|| 
|言語|Language|文字列|| 
|タイムゾーン|TimeZone|文字列|| 
|組織|DeptCode|文字列|| 
|姓名並び順|FirstAndLastNameOrder|数値|| 
|説明|Body|文字列|| 
|最終ログイン日時|LastLogintime|文字列|テナント管理者のみ取得可能| 
|パスワード有効期限|PasswordExpirationTime|文字列|テナント管理者のみ取得可能| 
|パスワード変更日時|PasswordChangeTime|文字列|テナント管理者のみ取得可能| 
|ログイン回数|NumberOfLogins|数値|テナント管理者のみ取得可能| 
|ログイン失敗回数|NumberOfDenial|数値|テナント管理者のみ取得可能| 
|テナント管理者|TenantManager|真偽値|テナント管理者のみ取得可能| 
|無効|Disabled|真偽値|テナント管理者のみ取得可能| 
|ロック|Lockout|真偽値|テナント管理者のみ取得可能| 
|ロックカウンター|LockoutCounter|数値|テナント管理者のみ取得可能| 
|コメント|Comments|文字列|| 
|作成者|Creator|数値|ユーザIDが返されます| 
|更新者|Updator|数値|ユーザIDが返されます| 
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
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)