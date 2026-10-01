---
title: extendedSql
icon: material/alpha-o-box
category: サーバスクリプト
order: '80000'
status: ''
parts: ''
urlstring: sever-script-extended-sql
translationKey: sever-script-extended-sql
shortname: extendedSql
created: 2021-06-09
updated: 2023-08-22
---

## 概要

[サーバスクリプト](../index.md)で[APIから拡張SQLを実行](../../extended-features/extended-sql/extended-sql-api.md)と同様に設定した[拡張SQL](../../extended-features/extended-sql/index.md)を実行します。

## プロパティ

プロパティはありません。

## メソッド

|メソッド|概要|
|:---|:---|
|ExecuteDataSet|拡張SQLを実行しDataSetオブジェクトを取得します。|
|ExecuteTable|拡張SQLを実行しDataTableオブジェクトを取得します。|
|ExecuteRow|拡張SQLを実行し結果セットの先頭行のDataRowオブジェクトを取得します。|
|ExecuteScalar|拡張SQLを実行し結果セットの先頭行の最初の列を取得します。|
|ExecuteNonQuery|拡張SQLを実行します。結果を受け取りません。|

## 使用例

下記の例では[拡張SQL](../../extended-features/extended-sql/index.md) GetUserTop10 を呼び出し、取得した UserId と Name をログに出力します。拡張SQLのパラメータには、組織ID=7、無効フラグ=falseをセットしています。

##### JavaScript（サーバスクリプト）

```
let rows = extendedSql.ExecuteTable('GetUserTop10', '{"DeptId": 7, "Disabled": false}');
for (let row of rows){
    context.Log(row.UserId + ':' + row.Name);
}
```

##### JSON（拡張SQLの設定）

```
{
    "Name": "GetUserTop10",
    "Api": true
}
```

##### SQL（拡張SQL）※SQL Server

```
select top 10 "UserId", "Name" from "Users"
where "DeptId"=@DeptId and "Disabled"=@Disabled;
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：拡張機能：拡張SQL：APIから拡張SQLを実行する](../../extended-features/extended-sql/extended-sql-api.md)
-   [開発者ガイド：拡張機能：拡張SQL](../../extended-features/extended-sql/index.md)