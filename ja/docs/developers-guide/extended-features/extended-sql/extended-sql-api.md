---
title: 拡張SQL：APIから拡張SQLを実行する
category: 拡張機能
order: '0'
status: ''
parts: ''
urlstring: extended-sql-api
translationKey: extended-sql-api
shortname: APIから拡張SQLを実行,API
created: 2020-03-03
updated: 2024-09-13
---

## 概要

[API](../../api/basics/api.md)と[拡張SQL](index.md)を組み合わせてデータベースから直接データを取得したり更新したりすることができます。

## 注意事項

1. 誤って使用するとプリザンターが利用できなくなったり、データが壊れたりする可能性がありますので、十分なテストを行った上でご利用ください。
1. APIキーやセッションによるログイン確認は行いますが、テーブルへの権限チェックなどが行われないため、SQLの中で実施する必要があります。
1. [レコード取得API](../../api/table-operations/api-record-get-multi.md)と異なり、取得件数の上限はありません。そのため取得内容・条件によっては処理時間が非常に長くなる可能性がありますので、十分なテストを行った上でご利用ください。

## 制限事項

1. 拡張SQLのJSONファイルやSQLファイルを更新した後は「アプリケーションを再起動」するまで反映しません。
1. セキュリティ上の理由により拡張SQLはWeb画面から設定できません。

## 事前準備

APIの操作を行う前に[APIキーの作成](../../api/basics/api-key.md)を実施してください。

.jsonファイルにて以下の2項目は必須項目となります。

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Name|Sample|APIから実行させる際の名前を設定します。|
|Api|true|trueの場合APIからの実行を許可します。|

CommandTextに直接SQL文を記載できますが、SQL文が長文になる場合など、ファイルを分けることが可能です。
その場合のファイル名は以下の画像のように、.jsonファイルと同名.sqlとしてください。  
例)  
APItoSQL.json　←定義ファイル  
APItoSQL.json.sql　←SQL文  

![.jsonファイルと同名の.sqlファイルを配置した状態](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/2d01585929d44f339937c9873ba5293e.png)

## URL

下記のURLを使用します。  HTTPメソッドはPOSTです。  
http://{ServerName}/api/extended/sql    
"http://{ServerName}" の部分は、環境に合わせて編集してください。  

## リクエスト

下記例のようにParamsに入れたパラメータは@RefIDのように拡張SQLに渡すパラメータとして使用することができます。
標準で用意されている@_Uなどのパラメータも使用できます。

```json
{
    "ApiVersion": 1.1,
    "ApiKey": "XXXXXXXXXX...",
    "Name": "Sample",
     "Params": {
    	"RefID": 1
    }
}
```

## JSONファイル

APItoSQL.json
```json
{
    "Name": "Sample",
    "Api": true
}
```

## SQL文(外部ファイル)

APItoSQL.json.sql
```sql
SELECT [ReferenceId]
      ,[DeptId]
      ,[GroupId]
      ,[UserId]
      ,[Ver]
      ,[PermissionType]
  FROM [Implem.Pleasanter].[dbo].[Permissions]
  WHERE [ReferenceId]=@RefID
```

## レスポンス

テーブル内にはレコードの配列があり、レコード内はKey, ValueのHashでカラム名と値が入ってきます。  

```json
{
    "StatusCode": 200,
    "Response": {
        "Data": {
            "Table": [
                {
                    "ReferenceId": 1,
                    "DeptId": 0,
                    "GroupId": 0,
                    "UserId": 1,
                    "Ver": 1,
                    "PermissionType": 511
                },
                {
                    "ReferenceId": 1,
                    "DeptId": 0,
                    "GroupId": 0,
                    "UserId": 9,
                    "Ver": 1,
                    "PermissionType": 31
                },
                {
                    "ReferenceId": 1,
                    "DeptId": 0,
                    "GroupId": 0,
                    "UserId": 10,
                    "Ver": 1,
                    "PermissionType": 31
                },
                {
                    "ReferenceId": 1,
                    "DeptId": 0,
                    "GroupId": 1,
                    "UserId": 0,
                    "Ver": 1,
                    "PermissionType": 511
                }
            ]
        }
    }
}
```

複数のテーブルから値を取得した場合は以下のようなレスポンスとなります。  
Response.Data.Table （1つめのテーブル）  
Response.Data.Table1 （2つめのテーブル）  
Response.Data.Table2 （3つめのテーブル）

## ユーザを指定して実行する

操作対象のオブジェクトの所有者がImplem.Pleasanter_Ownerである場合、以下のようなエラーが発生します。

例）PostgreSQLでItemsテーブルへのInsertをUser権限で実行した場合
「"PostgresException: 42501: permission denied for sequence Items_ReferenceId_seq"」

これは、シーケンスオブジェクトの所有者がImplem.Pleasanter_Ownerであるのに対して、実行者がImplem.Pleasanter_Userであるためです。
APIから拡張SQLを実行する際に以下のように指定すると、Owner権限で実行することができます。

## JSONファイル

APItoSQL.json
```json
{
    "Name": "Sample",
    "Api": true,
    "DbUser": "Owner"
}
```

## 関連情報

-   [開発者ガイド：API](../../api/basics/api.md)
-   [開発者ガイド：拡張機能：拡張SQL](index.md)
-   [開発者ガイド：API：テーブル操作：複数レコード取得](../../api/table-operations/api-record-get-multi.md)
-   [開発者ガイド：API：APIキーの作成](../../api/basics/api-key.md)