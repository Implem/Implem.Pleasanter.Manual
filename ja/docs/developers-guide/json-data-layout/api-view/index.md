---
title: View
category: JSONデータレイアウト
order: '10000'
status: ''
parts: ''
urlstring: api-view
translationKey: api-view
shortname: JSONデータレイアウト：View
created: 2020-02-13
updated: 2025-04-24
---

## 概要

[API](../../api/basics/api.md)や[サーバスクリプト](../../server-script/index.md)でレコードを操作する際に、[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)や[ソート](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)を指定するJSON形式のデータレイアウトです。

## データレイアウト

|項目名/種類|プロパティ名|データ型|備考|
|:--|--|--|:--|
|未完了|Incomplete|真偽値|| 
|自分|Own|真偽値|| 
|期限が近い|NearCompletionTime|真偽値|| 
|遅延|Delay|真偽値|| 
|期限超過|Overdue|真偽値|| 
|検索|Search|文字列|| 
|列フィルタ|ColumnFilterHash|オブジェクト(文字列)|| 
|列フィルタ検索タイプ|ColumnFilterSearchTypes|列挙型||
|否定|ColumnFilterNegatives|配列(文字列)|**本プロパティを使用する場合は[否定フィルタを使用する](../../../managers-guide/manage-table/filter/table-management-filter-use-negative-filter.md)を有効化する必要があります。また、ユーザ、グループ、組織を選択肢に設定している項目には使用できません。**|
|ソート|ColumnSorterHash|オブジェクト(文字列)||
|-|ApiDataType|列挙型||
|-|ApiColumnKeyDisplayType|列挙型|<b>本プロパティは、ApiDataTypeが"KeyValues"の場合のみ有効になります。</b>|
|-|ApiColumnValueDisplayType|列挙型|<b>本プロパティは、ApiDataTypeが"KeyValues"の場合のみ有効になります。</b>|
|-|ApiColumnHash|オブジェクト(文字列)| <b>本プロパティは、ApiDataTypeが"KeyValues"の場合のみ有効になります。</b>|
|-|GridColumns|配列(文字列)|<b>本プロパティは、ApiDataTypeが"KeyValues"の場合のみ有効になります。</b>|
|-|MergeSessionViewFilters|真偽値|値が真の場合、APIで指定したフィルタ条件とセッションに存在するフィルタ条件をマージします。同じフィルタ条件が存在する場合APIで指定したフィルタ条件を優先します。<br />値が偽の場合、セッションに存在するフィルタ条件はマージしません。<br />本プロパティの省略時の初期設定値は偽です。|
|-|MergeSessionViewSorters|真偽値|値が真の場合、APIで指定したソート条件とセッションに存在するソート条件をマージします。同じソート条件が存在する場合APIで指定したソート条件を優先します。<br />値が偽の場合、セッションに存在するソート条件はマージしません。<br />本プロパティの省略時の初期設定値は偽です。|

### 利用方法

ColumnFilterおよびApiDataTypeの利用方法は、下記を参照してください。

[開発者ガイド：JSONデータレイアウト：View：ColumnFilterの指定方法](api-view-columnfilter.md)  
[開発者ガイド：JSONデータレイアウト：View：ApiDataTypeの指定方法](api-view-apidatatype.md)  

## 制限事項

使用するデータベースによって検索結果が異なる場合があります。

- SQL Server：LIKE句またはフルテキスト検索が使用されます。
- PostgreSQL：ILIKE句またはpg_trgmによるフルテキスト検索が使用されます。

## 関連情報

-   [開発者ガイド：API](../../api/basics/api.md)
-   [開発者ガイド：サーバスクリプト](../../server-script/index.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)
-   [テーブルの管理：フィルタ：否定フィルタを使用する](../../../managers-guide/manage-table/filter/table-management-filter-use-negative-filter.md)
-   [開発者ガイド：JSONデータレイアウト：View：ColumnFilterの指定方法](api-view-columnfilter.md)
-   [開発者ガイド：JSONデータレイアウト：View：ApiDataTypeの指定方法](api-view-apidatatype.md)
