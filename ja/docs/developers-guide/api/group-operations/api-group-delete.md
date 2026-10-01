---
title: グループ削除
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-group-delete
translationKey: api-group-delete
shortname: ''
created: 2020-07-30
updated: 2025-01-30
---

## 概要

APIを使用してグループを削除することができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。また、この機能はテナント管理者でないと行えないため、ユーザ管理からテナント管理者の設定を行ってください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/groups/{グループID}/delete (※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{グループID}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/groups/{グループID}/delete 

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "l3ghls083sasA62Ssa32..."
}
```

## レスポンス

下記の形式のjsonデータが返却されます。  

##### JSON

``` 
{
    "Id": 12345,
    "StatusCode": 200,
    "Message": "\" 指定したグループ名 \" を削除しました。"
}
```  

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.24.0以降|機能追加|

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 仕様変更について

**※ 2019年10月よりAPIの仕様が一部変更となりました。**
- 分類, 数値, 日付, 説明, チェック項目はjsonにそのまま記載する方法から「～Hash」の中に記載する方法へ変更されました。

**※ 2018年11月よりAPIの仕様が一部変更となりました。**
- URLの形式が '/pleasanter/api_items/xxxx' から '/pleasanter/api/items/xxxx' に変更されました。
- Content-Type の指定が'application/x-www-form-urlencoded' から 'application/json'に変更されました。