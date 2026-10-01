---
title: ユーザ取得（選択）
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-user-get
translationKey: api-user-get
shortname: ''
created: 2019-10-11
updated: 2026-09-08
---

## 概要

APIを使用してユーザのレコードを取得することができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/users/get (※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/users/get

### (a)ユーザIDで特定のユーザ情報を取得する場合

##### JSON  

```
{
    "ApiVersion": 1.1,
    "ApiKey": "sad610bHDo04720DoloA356...",
    "View": {
        "ColumnFilterHash": {
            "UserId": "[11,12]"
        }
    }
}
```
UserIdによるフィルタは、複数の値を指定可能な配列となっておりますので上記のように記述してください。

### (b)条件を指定して一致するユーザ情報を取得する場合

##### JSON  

```
{
    "ApiVersion": 1.1,
    "ApiKey": "1ao3ea5kDH2335sar529UY...",
    "View": {
        "ColumnFilterHash": {
            "DeptId": "[7,8]",
            "Groups": "[1,2]",
            "Gender": "[2]"
        }
    }
}
```

## レスポンス

下記の形式のjsonデータが選択したUserIdの数だけ返却されます。  データのレイアウトは[こちら](../../json-data-layout/api-user.md)を参照してください(パスワードは取得できません)。  

以下の項目はテナント管理者のAPIキーで実行した場合のみ出力されます。

|出力項目|画面上の表示名|
|:--|:--|
|LastLoginTime|最終ログイン日時|
|PasswordExpirationTime|パスワード有効期限|
|PasswordChangeTime|パスワード変更日時
|NumberOfLogins|ログイン回数|
|NumberOfDenial|ログイン失敗回数|
|TenantManager|テナント管理者|
|Disabled|無効|
|Lockout|ロック|
|LockoutCounter|ロックカウンター|

###  (a) テナント管理者のAPIキーで実行した場合 

##### JSON  

```
{
    "StatusCode": 200,
    "Response": {
        "Offset": 0,
        "PageSize": 200,
        "TotalCount": 1,
        "Data": [
            {
                "TenantId": 12345,
                "UserId": 12345,
                "Ver": 1,
                "LoginId": "hayato",
                "GlobalId": "",
                "Name": "中野 隼人",
                "UserCode": "",
                "Birthday": "2016-03-27T00:00:00",
                "Gender": "",
                "Language": "ja",
                "TimeZone": "Tokyo Standard Time",
                "DeptCode": "",
                "DeptId": 0,
                "Theme": "",
                "Body": "",
                "LastLoginTime": "2023-08-17T12:00:00",
                "PasswordExpirationTime": "2023-08-31T12:00:00",
                "PasswordChangeTime": "2023-06-02T12:00:00",
                "NumberOfLogins": 100,
                "NumberOfDenial": 5,
                "TenantManager": false,
                "Disabled": false,
                "Lockout": false,
                "LockoutCounter": 0,
                "UserSettings": "{}",
                "SecondaryAuthenticationCode": "",
                "SecondaryAuthenticationCodeExpirationTime": "1899-12-30T00:00:00",
                "LdapSearchRoot": "",
                "SynchronizedTime": "1899-12-30T00:00:00",
                "Comments": "[]",
                "Creator": 2,
                "Updator": 1,
                "CreatedTime": "2023-04-01T12:00:00",
                "UpdatedTime": "2023-08-15T12:00:00",
                "MailAddresses": [
                    "webmaster@example.com",
                    "info@example.com"
                ],
                "ApiVersion": 1.1,
                "ClassHash": {
                },
                "NumHash": {
                },
                "DateHash": {
                },
                "DescriptionHash": {
                },
                "CheckHash": {
                },
                "AttachmentsHash": {
                }
            }
        ]
    }
}
```

### (b) テナント管理者以外のAPIキーで実行した場合  

##### JSON  

```
{
    "StatusCode": 200,
    "Response": {
        "Offset": 0,
        "PageSize": 200,
        "TotalCount": 1,
        "Data": [
            {
                "TenantId": 12345,
                "UserId": 12345,
                "Ver": 1,
                "LoginId": "hayato",
                "GlobalId": "",
                "Name": "中野 隼人",
                "UserCode": "",
                "Birthday": "2016-03-27T00:00:00",
                "Gender": "",
                "Language": "ja",
                "TimeZone": "Tokyo Standard Time",
                "DeptCode": "",
                "DeptId": 0,
                "Theme": "",
                "Body": "",
                "UserSettings": "{}",
                "SecondaryAuthenticationCode": "",
                "SecondaryAuthenticationCodeExpirationTime": "1899-12-30T00:00:00",
                "LdapSearchRoot": "",
                "SynchronizedTime": "1899-12-30T00:00:00",
                "Comments": "[]",
                "Creator": 2,
                "Updator": 1,
                "CreatedTime": "2023-04-01T12:00:00",
                "UpdatedTime": "2023-08-15T12:00:00",
                "MailAddresses": [
                    "webmaster@example.com",
                    "info@example.com"
                ],
                "ApiVersion": 1.1,
                "ClassHash": {
                },
                "NumHash": {
                },
                "DateHash": {
                },
                "DescriptionHash": {
                },
                "CheckHash": {
                },
                "AttachmentsHash": {
                }
            }
        ]
    }
}
```  

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 仕様変更について

**※ 2018年11月よりAPIの仕様が一部変更となりました。**
- URLの形式が '/pleasanter/api_items/xxxx' から '/pleasanter/api/items/xxxx' に変更されました。
- Content-Type の指定が'application/x-www-form-urlencoded' から 'application/json'に変更されました。