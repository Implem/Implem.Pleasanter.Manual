---
title: ユーザ更新
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-user-update
translationKey: api-user-update
shortname: ''
created: 2019-10-11
updated: 2026-09-08
---

## 概要

APIを使用してレコードを更新することができます。

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
|URL|http://{サーバ名}/api/users/{ユーザID}/update(※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{ユーザID}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/users/{ユーザID}/update

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "8s63Aiigd98h51Dfda7951...",
    "Name": "[更新後のユーザーの名前]",
    "MailAddresses": [
        "webmaster@example.com",
        "info@example.com"
    ]
}
```

※メールアドレスを更新する場合はMailAddressesにリスト形式で記述します（任意）。１つのユーザに対して単一または複数のメールアドレスを設定することが可能です。洗い替え方式で更新されます（古いメールアドレス情報を削除して新しいメールアドレス情報を追加する）。

## レスポンス

下記の形式のjsonデータが返却されます。  

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 200,
    "Message": "\" ユーザーの名前を更新 \" を更新しました。"
}
```

## メールアドレスの設定について

以下のようにMailAddressesのパラメータを指定した上でリストを空にした場合はメールアドレスが削除されます。

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "8s63Aiigd98h51Dfda7951...",
    "Name": "[更新後のユーザーの名前]",
    "MailAddresses": [
    ]
}
```

以下のようにMailAddressesのパラメータを指定しない場合はメールアドレスは更新（削除）されません。

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "8s63Aiigd98h51Dfda7951...",
    "Name": "[更新後のユーザーの名前]"
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.22.0 以降|メールアドレスをAPIで更新する機能を追加|

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 仕様変更について

**※ 2018年11月よりAPIの仕様が一部変更となりました。**
- URLの形式が '/pleasanter/api_items/xxxx' から '/pleasanter/api/items/xxxx' に変更されました。
- Content-Type の指定が'application/x-www-form-urlencoded' から 'application/json'に変更されました。