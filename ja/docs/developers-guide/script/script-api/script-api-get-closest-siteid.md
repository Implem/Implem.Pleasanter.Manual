---
title: $p.apiGetClosestSiteId
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-get-closest-siteid
translationKey: script-api-get-closest-siteid
shortname: $p.apiGetClosestSiteId,サイト名検索
created: 2024-06-05
updated: 2026-08-05
---

## 概要

AjaxのPOSTリクエストにより、[サイト名検索](../../api/site-operations/api-site-get-closest-siteid.md)で該当サイトに最も近いサイトIDを取得します。

## 前提条件

1. 本機能はサイトの「サイト名」を検索します。あらかじめサイト名を設定してください。サイトの[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)ではありませんので注意ください。
![サイトの「サイト名」を設定する箇所](https://pleasanter.org/files/images/ja/developers-guide/script/script-api/assets/be2492d00d0c4ee0b48cd62f3356ac73.png)

## 構文

##### JavaScript

```
$p.apiGetClosestSiteId({
    id: <検索開始のサイトID>,
    data: {
        <取得条件>
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
```

## 各パラメータの説明

|パラメータ名|説明|必須|
|:--|:--|:--:|
|id|検索開始のサイトID。通常は $p.siteId() を使用して、このメソッドを呼び出しているサイトのIDを指定します。|○|
|data|取得条件|○|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

## 取得条件について

|キーワード|説明|必須|
|:--|:--|:--:|
|FindSiteNames|検索したい対象のサイト名を配列で指定。|○|

## 使用例

### 呼び出し

##### JavaScript

```
$p.apiGetClosestSiteId({
    id: $p.siteId(),
    data: {
        FindSiteNames:['ParentSite','HideSize']
    },
    done: function (data) {
        console.log(data);
    }
});
``` 

### レスポンス

##### JSON

```
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

## 関連情報

-   [開発者ガイド：API：サイト操作：サイト名検索で該当サイトに最も近いサイトID取得](../../api/site-operations/api-site-get-closest-siteid.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../managers-guide/tenant-administration/tenant-logo.md)
