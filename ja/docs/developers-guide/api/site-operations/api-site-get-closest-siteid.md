---
title: サイト名検索で該当サイトに最も近いサイトID取得
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-site-get-closest-siteid
translationKey: api-site-get-closest-siteid
shortname: サイト名検索API,サイト名検索
created: 2024-06-05
updated: 2025-01-30
---

## 概要

APIを使用して「サイト名検索」で該当サイトに最も近いサイトIDを取得することができます。

## 前提条件

1.  本機能はサイトの「サイト名」を検索します。あらかじめサイト名を設定してください。サイトの[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)ではありませんので注意ください。

    ![サイトの「サイト名」を設定する箇所](https://pleasanter.org/files/images/ja/developers-guide/api/site-operations/assets/be2492d00d0c4ee0b48cd62f3356ac73.png)

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。また、この機能はテナント管理者でないと行えないため、ユーザ管理からテナント管理者の設定を行ってください。

## リクエスト

下記のリクエスト形式で、JSONデータを送信します。

| 設定項目     | 値                                                             |
| :----------- | :------------------------------------------------------------- |
| HTTPメソッド | POST                                                           |
| Content-Type | application/json                                               |
| 文字コード   | UTF-8                                                          |
| URL          | http://{サーバ名}/api/items/{サイトID}/getclosestsiteid [^1] |
| Body         | 以下のjsonデータを参考のこと                                   |

[^1]:
    {サーバ名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。  
    pleasanter.netの場合は以下の形式になります。  
    `https://pleasanter.net/fs/api/items/{サイトID}/getclosestsiteid`  
    {サイトID}には、サイト検索を開始する対象のサイトを指定してください。

``` json title="JSON" linenums="1"
{
    "ApiVersion": "1.1",
    "ApiKey": "345yuAjA6789dA09d8uj6...",
    "FindSiteNames": [
        "SiteName1",
        "SiteName2"
    ]
}
```

### FindSiteNamesについて

検索したい対象のサイト名を配列で指定します。

以下の例ではサイト名が"ParentSite","HideSite"を検索します。

``` json title="JSON" linenums="1"
{
    "ApiVersion": 1.1,
    "ApiKey": "345yuAjA6789dA09d8uj6...",
    "FindSiteNames": [
        "ParentSite",
        "HideSite"
    ]
}
```

## レスポンス

下記の形式のJSONデータが返却されます。

``` json title="JSON" linenums="1"
{
    "SiteId": 12345,
    "Data": [
        {
            "SiteName": "ParentSite",
            "SiteId": 12344
        },
        {
            "SiteName": "HideSite",
            "SiteId": -1
        }
    ]
}
```

検索対象サイト名と対となるSiteIdが返されます。  
見つからなかった場合またはアクセス権がなかった場合は-1を返却します。

スクリプトでの使用方法は、以下のマニュアルを参照してください。  
[$p.apiGetClosestSiteid](../../script/script-api/script-api-get-closest-siteid.md)

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.4.5.0以降    | 機能追加 |

## 関連情報

-   [FAQ：サイト名検索で該当サイトに最も近いサイトID取得の検索順が知りたい。](../../../FAQ/features-for-developers/faq-get-closest-site-logic.md)
