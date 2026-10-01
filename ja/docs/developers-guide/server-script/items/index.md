---
title: items
icon: material/alpha-o-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items
translationKey: server-script-items
shortname: items,itemsオブジェクト
created: 2021-01-27
updated: 2026-06-29
---

## 概要

[サーバスクリプト](../index.md)で「レコード」の作成、読み取り、更新、削除等を行うためのオブジェクトです。「modelオブジェクト」では現在のレコードのみを扱えますが、「itemsオブジェクト」ではIDを指定して任意のレコードを扱うことができます。

## 注意事項

1. [サーバスクリプト](../index.md)で「レコード」のI/Oを行うとサーバ側の処理負荷が増大することがあります。[サーバスクリプト](../index.md)の実行時間が 指定した処理タイムアウト時間を超えるとタイムアウトにより処理が停止し「アプリケーションエラー」が発生します。タイムアウト時間の調整は[Script.json](../../../setup/parameters/script-json.md)の「ServerScriptTimeOut」で行います。

## 制限事項

1. アクセス権の無い操作を行うことはできません。例えば レコードID 10 の読み取り操作を行うスクリプトを記述した場合、レコードID 10 の読み取り権限のないユーザがアクセスした場合には、レコードの取得が行えません。

## プロパティ

プロパティはありません。

## メソッド

|No|Name|Description|
|:---|:---|:---|
|1|[Average](server-script-items-average.md)|「レコード」の[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)の平均値を取得します。| 
|2|[BulkDelete](server-script-items-bulk-delete.md)|「レコード」を一括削除します。|
|3|[Count](server-script-items-count.md)|「レコード」の件数を取得します。| 
|4|[Create](server-script-items-create.md)|「レコード」を作成します。|
|5|[Delete](server-script-items-delete.md)|「レコード」を削除します。|
|6|[Get](server-script-items-get.md)|指定した条件に合致する[apiModel](../apiModel/server-script-api-model-create.md)オブジェクトの配列を取得します。|
|7|[GetClosestSite](server-script-items-get-closest-site.md)|サイトのサイト名を指定して該当サイトに最も近いサイト情報を取得します。| 
|8|[GetSite](server-script-items-get-site.md)|サイトIDを指定してサイト情報を取得します。| 
|9|[GetSiteByGroupName](server-script-items-get-site-by-group-name.md)|サイトのサイトグループ名を指定してサイト情報を取得します。| 
|10|[GetSiteByName](server-script-items-get-site-by-name.md)|サイトのサイト名を取得してサイト情報を取得します。| 
|11|[GetSiteByTitle](server-script-items-get-site-by-title.md)|サイトのタイトルを指定してサイト情報を取得します。| 
|12|[Max](server-script-items-max.md)|「レコード」の[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)の最大値を取得します。| 
|13|[MaxDate](server-script-items-maxdate.md)|「レコード」の[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)の最大値を取得します。| 
|14|[Min](server-script-items-min.md)|「レコード」の[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)の最小値を取得します。| 
|15|[MinDate](server-script-items-mindate.md)|「レコード」の[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)の最小値を取得します。| 
|16|[NewIssue](server-script-items-new-issue.md)|「期限付きテーブル」に対する[apiModel](../apiModel/server-script-api-model-create.md)オブジェクトの新規インスタンスを作成します。|
|17|[NewResult](server-script-items-new-result.md)|「記録テーブル」に対する[apiModel](../apiModel/server-script-api-model-create.md)オブジェクトの新規インスタンスを作成します。|
|18|[NewSite](server-script-items-new-site.md)|[サイト](../../../users-guide/site/index.md)に対する[apiModel](../apiModel/server-script-api-model-create.md)オブジェクトの新規インスタンスを作成します。|
|19|[Sum](server-script-items-sum.md)|「レコード」の[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)の合計値を取得します。| 
|20|[Update](server-script-items-update.md)|「レコード」を更新します。|
|21|[Upsert](server-script-items-upsert.md)|指定したサイトでキー項目に該当する「レコード」が存在する場合は更新し、存在しない場合は新規作成します。|
|22|[New（非推奨）](server-script-items-new.md)|「期限付きテーブル」に対する[apiModel](../apiModel/index.md)オブジェクトの新規インスタンスを作成します。|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)
-   [開発者ガイド：サーバスクリプト：items.NewIssue](server-script-items-new-issue.md)
-   [開発者ガイド：サーバスクリプト：apiModel.Create](../apiModel/server-script-api-model-create.md)
-   [開発者ガイド：サーバスクリプト：items.NewResult](server-script-items-new-result.md)
-   [開発者ガイド：サーバスクリプト：items.NewSite](server-script-items-new-site.md)
-   [サイト機能](../../../users-guide/site/index.md)
-   [開発者ガイド：サーバスクリプト：items.Create](server-script-items-create.md)
-   [開発者ガイド：サーバスクリプト：items.Get](server-script-items-get.md)
-   [開発者ガイド：サーバスクリプト：items.Update](server-script-items-update.md)
-   [開発者ガイド：サーバスクリプト：items.Delete](server-script-items-delete.md)
-   [開発者ガイド：サーバスクリプト：items.BulkDelete](server-script-items-bulk-delete.md)
-   [開発者ガイド：サーバスクリプト：items.Sum](server-script-items-sum.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [開発者ガイド：サーバスクリプト：items.Average](server-script-items-average.md)
-   [開発者ガイド：サーバスクリプト：items.Max](server-script-items-max.md)
-   [開発者ガイド：サーバスクリプト：items.Min](server-script-items-min.md)
-   [開発者ガイド：サーバスクリプト：items.Count](server-script-items-count.md)
-   [開発者ガイド：サーバスクリプト：items.GetSite](server-script-items-get-site.md)
-   [開発者ガイド：サーバスクリプト：items.GetSiteByTitle](server-script-items-get-site-by-title.md)
-   [開発者ガイド：サーバスクリプト：items.GetSiteByName](server-script-items-get-site-by-name.md)
-   [開発者ガイド：サーバスクリプト：items.GetSiteByGroupName](server-script-items-get-site-by-group-name.md)
-   [開発者ガイド：サーバスクリプト：items.GetClosestSite](server-script-items-get-closest-site.md)
-   [開発者ガイド：サーバスクリプト：items.MaxDate](server-script-items-maxdate.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [開発者ガイド：サーバスクリプト：items.MinDate](server-script-items-mindate.md)