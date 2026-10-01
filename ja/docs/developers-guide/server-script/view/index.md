---
title: view
icon: material/alpha-o-box
category: サーバスクリプト
order: '4000'
status: ''
parts: ''
urlstring: server-script-view
translationKey: server-script-view
shortname: view
created: 2021-10-18
updated: 2026-06-29
---

## 概要

[サーバスクリプト](../index.md)で[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)の指定を行うためのオブジェクトです。「レコード」の[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)や[ソート](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)を行うことが可能です。

## 制限事項

1. 「ビュー処理時」の条件のみ使用できます。

## プロパティ

|No|Name|Get|Set|Type|Description|
|:----|:----|:----|:----|:----|:----|
|1|[AlwaysGetColumns](server-script-view-always-get-columns.md)|○|○|Dictionary<string, string>|画面上にない[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)を「modelオブジェクト」に読み込む指定|
|2|[FilterNegative](server-script-view-filter-negative.md)|○|○|Dictionary<string, bool>|[否定](../../../users-guide/table/record-authoring/data-analysis/table-record-negative-search.md)の指定|
|3|[Filters](server-script-view-filters.md)|○|○|Dictionary<string, string>|[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)の指定|
|4|[FiltersCleared](server-script-view-filters-cleared.md)|○|✕|bool|view.ClearFilters()が呼び出されていればtrue|
|5|[Id](server-script-view-id.md)|○|✕|int|現在の[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)の取得|
|6|[OnSelectingWhere](server-script-view-on-selecting-where.md)|○|○|string|[拡張SQL](../../extended-features/extended-sql/index.md)の[OnSelectingWhere](../../../FAQ/grid/faq-extended-sql-selecting-where.md)を動的に指定|
|7|[SearchTypes](server-script-view-search-types.md)|○|○|Dictionary<string, string>|「検索方法」の指定|
|8|[Sorters](server-script-view-sorters.md)|○|○|Dictionary<string, string>|[ソート](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)の指定|

## メソッド

|No|Name|Description|
|:----|:----|:----|
|1|[AddColumnPlaceholder](server-script-view-add-column-placeholder.md)|[拡張SQL](../../extended-features/extended-sql/index.md)の[OnSelectingWhere](../../../FAQ/grid/faq-extended-sql-selecting-where.md)のプレースホルダに動的な[カラム名](../../dev-column-name.md)を指定します。|
|2|[ClearFilters](server-script-view-clear-filters.md)|設定されているフィルタ条件をクリア。|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [応用編：ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)
-   [開発者ガイド：サーバスクリプト：view.Id](server-script-view-id.md)
-   [開発者ガイド：サーバスクリプト：view.AlwaysGetColumns](server-script-view-always-get-columns.md)
-   [テーブルの管理：項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [開発者ガイド：サーバスクリプト：view.OnSelectingWhere](server-script-view-on-selecting-where.md)
-   [開発者ガイド：拡張機能：拡張SQL](../../extended-features/extended-sql/index.md)
-   [FAQ：一覧表示するレコードを所属組織別に分けたい](../../../FAQ/grid/faq-extended-sql-selecting-where.md)
-   [開発者ガイド：サーバスクリプト：view.Filters](server-script-view-filters.md)
-   [開発者ガイド：サーバスクリプト：view.FilterNegative](server-script-view-filter-negative.md)
-   [テーブル機能：レコードの否定条件の検索（フィルタ）](../../../users-guide/table/record-authoring/data-analysis/table-record-negative-search.md)
-   [開発者ガイド：サーバスクリプト：view.SearchTypes](server-script-view-search-types.md)
-   [開発者ガイド：サーバスクリプト：view.Sorters](server-script-view-sorters.md)
-   [開発者ガイド：サーバスクリプト：view.FiltersCleared](server-script-view-filters-cleared.md)
-   [開発者ガイド：サーバスクリプト：view.ClearFilters](server-script-view-clear-filters.md)