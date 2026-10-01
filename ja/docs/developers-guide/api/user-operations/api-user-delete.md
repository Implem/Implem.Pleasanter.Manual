---
title: ユーザ削除
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-user-delete
translationKey: api-user-delete
shortname: ''
created: 2019-10-11
updated: 2023-08-17
---

## 概要

APIを使用してレコードを削除することができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。  
また、この機能はテナント管理者でないと行えないため、ユーザ管理からテナント管理者の設定を行ってください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/users/{ユーザID}/delete(※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{ユーザID}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/users/{ユーザID}/delete

##### JSON  

```
{
    "ApiVersion": 1.1,
    "ApiKey": "620fhk448A3fa467dA816..."
}
```

## レスポンス

下記の形式のjsonデータが返却されます。  

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 200,
    "Message": "\" 指定したユーザ名 \" を削除しました。"
}
```

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 仕様変更について

**※ 2018年11月よりAPIの仕様が一部変更となりました。**
- URLの形式が '/pleasanter/api_items/xxxx' から '/pleasanter/api/items/xxxx' に変更されました。
- Content-Type の指定が'application/x-www-form-urlencoded' から 'application/json'に変更されました。