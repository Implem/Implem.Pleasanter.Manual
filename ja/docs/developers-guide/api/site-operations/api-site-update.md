---
title: サイト更新
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-site-update
translationKey: api-site-update
shortname: ''
created: 2022-04-15
updated: 2026-08-26
---

## 概要

APIを使用してサイト設定を更新することができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。また、この機能はテナント管理者でないと行えないため、ユーザ管理からテナント管理者の設定を行ってください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{サイトID}/updatesite(※1)| 
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{サイトID}/updatesite  
　　{サイトID}には、更新対象のサイトIDを指定してください。

##### JSON

```
{
    "ApiVersion": "1.1",
    "ApiKey": "345yuAjA6789dA09d8uj6...",
    "TenantId": 1,
    "Title": "サイト名",
    "ReferenceType": "Issues",
    "ParentId": 99999,
    "InheritPermission": 99999,
    "SiteSettings": {
        "Version": 1.017,
        "ReferenceType": "Issues",
        "GridColumns": [
            "IssueId",
            "TitleBody",
            "Comments",
            "StartTime",
            "CompletionTime",
            "WorkValue",
            "ProgressRate",
            "RemainingWorkValue",
            "Status",
            "Manager",
            "Owner",
            "Updator",
            "UpdatedTime"
        ],
        "EditorColumnHash": {
            "General": [
                "IssueId",
                "Ver",
                "Title",
                "Body",
                "StartTime",
                "CompletionTime",
                "WorkValue",
                "ProgressRate",
                "RemainingWorkValue",
                "Status",
                "Manager",
                "Owner",
                "Comments"
            ]
        }
    }
}
```
※TenantID以降のパラメータについては、サイトパッケージをエクスポートした際の、"Site”パラメータと同等の値を設定してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.4.0 以降|機能追加|
