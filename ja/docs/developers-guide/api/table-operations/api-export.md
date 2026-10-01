---
title: テーブルのエクスポート
category: API
order: '2000'
status: ''
parts: ''
urlstring: api-export
translationKey: api-export
shortname: エクスポート
created: 2019-12-17
updated: 2026-07-14
---

## 概要

APIを使用して指定したテーブルのエクスポートを行うことができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{サイトID}/export (※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{サイトID}/export  

### (a) 標準のエクスポート設定でテーブルをエクスポートする  

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "3da0fa3a7R61faf821..."
}
```  

### (b) Pleasanterで作成済みのエクスポート設定を使用してテーブルをエクスポートする  

[テーブルの管理](../../../managers-guide/manage-table/index.md)の「エクスポート」タブにて作成したエクスポート設定を使用してエクスポートを行うことができます。  
設定ファイルのJSONにて、APIキーの他に作成したエクスポート設定のIDを指定します。  

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "6a7D132dgssDsg04GDS73...",
    "ExportId": 1
}
```

### (c) エクスポートの設定を設定ファイルに直接記述してテーブルをエクスポートする  

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "60gds37dF4fds2D...",
    "Export": {
        "Name": "テストA-1",
        "Columns": [
            {
                "ColumnName": "Title"
            },
            {
                "ColumnName": "Body"
            }
        ],
        "Header": false,
        "Type": "csv"
    }
}
```

- Name: エクスポート設定の名前  
- Columns: 出力対象となる項目の項目名  
- Header: 出力するCSVにヘッダ行を追加するか否かの設定です  
- Type: 出力するファイルの種類を指定します。指定できるのは「csv」と「json」の2種類です。  

### (d) 取得するレコードの絞り込みや並び順を指定してエクスポートする

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "61dsf0D8D4g2DE4df23...",
    "ExportId": 1,
    "View": {
        "ColumnSorterHash": {
            "Title": "desc"
        },
        "ColumnFilterHash": {
            "Owner": "[1]"
        }
    }
}
```

## レスポンス

下記の形式のjsonデータが返却されます。  

##### JSON

```
{
    "StatusCode": 200,
    "LimitPerDate": 10000,
    "LimitRemaining": 9990,
    "Response": {
        "Name": "期限付きテーブル_20xx_xx_xx xx_xx_xx.Csv",
        "Content": "\"ID\",\"タイトル\",\"内容\",\"タイトル/内容\",\"コメント\".........."
    }
}
```

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 関連情報

-   [テーブルの管理](../../../managers-guide/manage-table/index.md)