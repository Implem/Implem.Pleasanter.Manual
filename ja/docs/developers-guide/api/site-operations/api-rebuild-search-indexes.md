---
title: 検索インデックス再構築
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-rebuild-search-indexes
translationKey: api-rebuild-search-indexes
shortname: 検索インデックス再構築
created: 2023-03-28
updated: 2023-08-17
---

## 概要

APIで検索インデックスの再構築ができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。また、この機能はテナント管理者でないと行えないため、ユーザ管理からテナント管理者の設定を行ってください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

| 設定項目     | 値                                                                          |
| :----------- | :-------------------------------------------------------------------------- |
| HTTPメソッド | POST                                                                        |
| Content-Type | application/json                                                            |
| 文字コード   | UTF-8                                                                       |
| URL          | http://{サーバ名}/api/backgroundtasks/{サイトID}/rebuildsearchindexes(※1) |
| Body         | 下記JSONデータを参照                                                        |

(※1){サーバ名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "xxxxx..."
}
```

## レスポンス

成功した場合は以下のレスポンスが返却されます。

##### JSON

```
{
    "Id": 1,
    "StatusCode": 200,
    "Message": "検索インデックスの再構築が完了しました。"
}
```
