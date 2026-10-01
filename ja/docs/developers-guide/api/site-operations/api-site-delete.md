---
title: サイト削除
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-site-delete
translationKey: api-site-delete
shortname: ''
created: 2022-04-15
updated: 2026-09-11
---

## 概要

APIを使用してサイトを削除することができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。また、この機能はテナント管理者でないと行えないため、ユーザ管理からテナント管理者の設定を行ってください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{サイトID}/deletesite(※１)| 
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{サイトID}/deletesite  
　　{サイトID}には、削除対象のサイトIDを指定してください。

##### JSON

```
{
    "ApiVersion": "1.1",
    "ApiKey": "345yuAjA6789dA09d8uj6..."
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.4.0 以降|機能追加|
