---
title: ApiDataTypeの指定方法
category: JSONデータレイアウト
order: '10000'
status: ''
parts: ''
urlstring: api-view-apidatatype
translationKey: api-view-apidatatype
shortname: ''
created: 2025-07-14
updated: 2026-10-01
---

## 概要

[API](../../api/basics/api.md)や「[サーバスクリプト](../../server-script/index.md)」でレコードを操作する際、JSON形式フォーマットで各種オプションを指定します。

## ApiDataTypeの指定方法

返却されるレスポンスの各項目の形式を指定します。

|設定値|動作|
|:---|:---|
|"KeyValues"|返却されるレスポンスの各項目の形式が表示名となります。|
|指定なし(既定値)|Keyはカラム名、Valueは値(データベース上に登録されている値)|

```JSON
ApiDataType: "KeyValues"
```

- "GridColumns"を指定しない場合は、「[テーブルの管理](../../../managers-guide/manage-table/index.md)」の「[一覧](../../../managers-guide/manage-table/grid/index.md)」タブで有効化された項目が取得されます。

## ApiColumnKeyDisplayTypeの指定方法

返却されるレスポンスの各項目のKeyの表示形式を指定します。

|設定値|Keyの表示形式|
|:---|:---|
|"LabelText"|表示名 (既定値)|
|"ColumnName"|カラム名|

```JSON
ApiColumnKeyDisplayType: "ColumnName"
```

※ **本プロパティは、ApiDataTypeが"KeyValues"の場合のみ有効になります。**

## ApiColumnValueDisplayTypeの指定方法

返却されるレスポンスの各項目のValueの表示形式を指定します。

|設定値|Valueの表示形式|
|:---|:---|
|"DisplayValue"|表示名 (規定値)|
|"Value"|値(データベース上に登録されている値)|
|"Text"|設定した書式や単位等も含めた値|

```JSON
ApiColumnValueDisplayType: "DisplayValue"
```

※ **本プロパティは、ApiDataTypeが"KeyValues"の場合のみ有効になります。**

## ApiColumnHashの指定方法

項目単位で、Key・Valueの表示形式を指定します。各項目ごとに、Keyは<b>"KeyDisplayType"</b>、Valueは<b>"ValueDisplayType"</b>で指定します。

keyの表示形式を指定する

|KeyDisplayType|keyの表示形式|
|:---|:---|
|"LabelText"|表示名(規定値)|
|"ColumnName"|カラム名|

Valueの表示形式を指定する

|ValueDisplayType|Valueの表示形式|
|:---|:---|
|"DisplayValue"|表示名 (規定値)|
|"Value"|値(データベース上に登録されている値)|
|"Text"|設定した書式や単位等も含めた値|

（例）更新者(Updator)の値の表示形式を表示名にしたいとき 
```JSON
ApiColumnHash: {
    Updator: {
        ValueDisplayType: "DisplayValue"
    }
}
```

※ **本プロパティは、ApiDataTypeが"KeyValues"の場合のみ有効になります。**

## GridColumnsの指定方法

返却される項目を配列形式で指定します。

```JSON
GridColumns: ["ClassA","ClassB"]
```

"GridColumns"を指定しない場合は、「[テーブルの管理](../../../managers-guide/manage-table/index.md)」の「[一覧](../../../managers-guide/manage-table/grid/index.md)」タブで有効化された項目が取得されます。

### 親テーブル側の項目を指定する 

次のように記述します。

- 親テーブル（サイトID：11）の分類Bの値を取得します。
- 子テーブルの分類Aがリンク設定されています。

```JSON
GridColumns: ["ClassA","ClassA~11,ClassB"]
```

※ **本プロパティは、ApiDataTypeが"KeyValues"の場合のみ有効になります。**

## 制限事項

使用するデータベースによって検索結果が異なる場合があります。

- SQL Server：LIKE句またはフルテキスト検索が使用されます。
- PostgreSQL：ILIKE句またはpg_trgmによるフルテキスト検索が使用されます。
