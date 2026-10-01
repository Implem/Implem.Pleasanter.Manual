---
title: サイト設定のキャッシュ
category: API
order: '0'
status: ''
parts: ''
urlstring: api-sitesettings-activate
translationKey: api-sitesettings-activate
shortname: ''
created: 2026-06-11
updated: 2026-06-11
---

## 概要

「サイト設定のキャッシュ有効化」をAPIで制御します。

## 制限事項

1. Enterprise Editionのライセンスが必要です。Enterprise Editionは有償の年間サポートサービスの契約により利用可能です。

## 前提条件

1. APIを使用するためには「[APIキー](../basics/api-key.md)」を作成する必要があります。
1. ログインしているブラウザのセッションからアクセスする場合には「APIキー」を指定せずに使用可能です。

## 操作手順

APIリクエストでサイト設定のキャッシュを使用する場合は、リクエストボディにSsCacheを追加し、trueを指定します。

##### JSON

```json
{
     "ApiVersion": 1.1,
     "ApiKey": "63Kfk0ds3d4S2DBsa32...",
     "SsCache": true
}
```

SsCacheを省略した場合、またはfalseを指定した場合は、サイト設定のキャッシュを使用しません。
