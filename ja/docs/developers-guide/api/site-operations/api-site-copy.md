---
title: サイトコピー
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-site-copy
translationKey: api-site-copy
shortname: ''
created: 2022-04-26
updated: 2025-01-30
---

## 概要

APIを使用してサイト設定を更新することができます。

## 制限事項

1. 期限付きテーブルおよび、記録テーブルのみ使用可能です。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。また、この機能はテナント管理者でないと行えないため、ユーザ管理からテナント管理者の設定を行ってください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{サイトID}/copysitepackage(※1)| 
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{サイトID}/copysitepackage
　　{サイトID}には、コピーするサイトのうちタイトル更新対象のサイトIDを指定してください。

##### JSON

```
{
    "ApiVersion": "1.1",
    "ApiKey": "345yuAjA6789dA09d8uj6...",
    "TargetSiteId": 466220,
    "SiteTitle": "test",
    "SelectedSites": [
        {
            "SiteId": 466217
        },        
        {
            "SiteId": 466218,
            "IncludeData": false
        }
    ],
    "IncludeSitePermission": false,
    "IncludeRecordPermission": true,
    "IncludeColumnPermission": false,
    "IncludeNotifications": true,
    "IncludeReminders": true
}
```

|カラム|設定内容|
|:--|:--|  
|TargetSiteId|Copy先のフォルダのサイトIDを指定します。省略する場合、トップ画面にコピーします。|
|SiteTitle|URLの{サイトID}に記載したサイトのタイトルを指定します。サイトのタイトルを変更する場合に使用してください。|
|SelectedSites|コピーするサイトを指定します。記載方法は、サイトパッケージをエクスポートした際の"Convertors"パラメータと同等の値を設定してください。|

※IncludeSitePermission以降のパラメータについては、サイトパッケージをエクスポートした際の、"HeaderInfo"パラメータと同等の値を設定してください。

## レスポンス

下記の形式のjsonデータが返却されます。 

##### JSON

```
{
	"StatusCode": 200,
	"Response": {
		"Data": "[
			{\"OldSiteId\":466217,\"NewSiteId\":466221,\"ReferenceType\":\"Sites\",\"Title\":\"test\"},
			{\"OldSiteId\":466218,\"NewSiteId\":466222,\"ReferenceType\":\"Results\",\"Title\":\"記録テーブル\"}
		]"
	}
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.2.8 以降|機能追加|
