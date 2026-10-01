---
title: 組織取得
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-dept-get
translationKey: api-dept-get
shortname: ''
created: 2019-12-23
updated: 2026-09-08
---

## 概要

APIを使用してレコードの内容を取得することができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト  

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/depts/get (※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/depts/get

### 組織情報を取得する場合

##### JSON  

```
{
     "ApiVersion": 1.1,
     "ApiKey": "dD32ai53j3asdK2fre..."
}
```

### 条件を指定して一致する組織情報を取得する場合

##### JSON  

```
{
    "ApiVersion": 1.1,
    "ApiKey": "1ao3ea5kDH2335sar529UY...",
    "View": {
        "ColumnFilterHash": {
            "Groups": "[1,2]"
        }
    }
}
```
上の例は、グループIDが1または2のグループに含まれる組織が取得されます。

## レスポンス

下記の形式のjsonデータが返却されます。
Response部分のデータのレイアウトは[こちら](../../json-data-layout/api-dept.md)を参照してください。  

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
                "TenantId": 1,
                "DeptId": 1,
                "Ver": 1,
                "DeptCode": "1234",
                "DeptName": "システム開発部",
                "Body": "",
                "Disabled": false,
                "Comments": "[]",
                "Creator": 1,
                "Updator": 1,
                "CreatedTime": "2023-04-01T12:00:00",
                "UpdatedTime": "2023-08-15T12:00:00",
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

**※ 2019年10月よりAPIの仕様が一部変更となりました。**
- 分類, 数値, 日付, 説明, チェック項目はjsonにそのまま記載する方法から「～Hash」の中に記載する方法へ変更されました。　　

**※ 2018年11月よりAPIの仕様が一部変更となりました。**
- URLの形式が '/pleasanter/api_items/xxxx' から '/pleasanter/api/items/xxxx' に変更されました。
- Content-Type の指定が'application/x-www-form-urlencoded' から 'application/json'に変更されました。