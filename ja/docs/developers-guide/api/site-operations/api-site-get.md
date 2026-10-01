---
title: サイト取得
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-site-get
translationKey: api-site-get
shortname: ''
created: 2022-04-15
updated: 2026-09-11
---

## 概要

APIを使用してサイト情報を取得することができます。

## 制限事項

wikiには対応していません。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。また、この機能はテナント管理者でないと行えないため、ユーザ管理からテナント管理者の設定を行ってください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{サイトID}/getsite(※１)| 
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{サイトID}/getsite  
　　{サイトID}には、取得対象のサイトIDを指定してください。

##### JSON

```
{
    "ApiVersion": "1.1",
    "ApiKey": "345yuAjA6789dA09d8uj6..."
}
```

## レスポンス

下記の形式のJSONデータが返却されます。

##### JSON  

```
{
    "StatusCode": 200,
    "Response": {
        "Data": {
            "TenantId": 1,
            "SiteId": 12345,
            "UpdatedTime": "2023-08-17T12:00:00",
            "Ver": 1,
            "Title": "記録テーブル",
            "Body": "",
            "SiteName": "",
            "SiteGroupName": "",
            "GridGuide": "",
            "EditorGuide": "",
            "CalendarGuide": "",
            "CrosstabGuide": "",
            "GanttGuide": "",
            "BurnDownGuide": "",
            "TimeSeriesGuide": "",
            "KambanGuide": "",
            "ImageLibGuide": "",
            "ReferenceType": "Results",
            "ParentId": 12344,
            "InheritPermission": 3301,
            "Permissions": [
            ],
            "SiteSettings": {
                "Version": 1.017,
                "ReferenceType": "Results",
                "EditorColumnHash": {
                    "General": [
                        "ResultId",
                        "Ver",
                        "Title",
                        "Body",
                        "Status",
                        "Manager",
                        "Owner",
                        "Comments",
                        "ClassA",
                        "ClassB",
                        "ClassC"
                    ]
                },
                "NoDisplayIfReadOnly": false
            },
            "Publish": false,
            "DisableCrossSearch": false,
            "LockedTime": "1899-12-30T00:00:00",
            "LockedUser": 0,
            "ApiCountDate": "1899-12-30T00:00:00",
            "ApiCount": 0,
            "Comments": "[]",
            "Creator": 1,
            "Updator": 1,
            "CreatedTime": "2023-08-17T09:00:00",
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
    }
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.4.0 以降|機能追加|
