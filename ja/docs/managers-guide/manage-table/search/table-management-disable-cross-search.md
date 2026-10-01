---
title: 横断検索を無効化
category: 検索
order: '1050'
status: ''
parts: ''
urlstring: table-management-disable-cross-search
translationKey: table-management-disable-cross-search
shortname: 横断検索を無効化
created: 2021-11-04
updated: 2025-01-30
---

## 概要

対象の[テーブル](../../../users-guide/table/index.md)が[横断検索](../../../users-guide/common/crosssearch.md)で検索できないように設定します。[拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)の[OnSelectingWhere](../../../FAQ/grid/faq-extended-sql-selecting-where.md)や[サーバスクリプト](../../../developers-guide/server-script/index.md)の[view.Filters](../../../developers-guide/server-script/view/server-script-view-filters.md)で[レコードのアクセス制御](../../../users-guide/access-control/table-record-access-control.md)を行っている場合、本チェックをオンにします。これらの機能で一覧画面でレコードを非表示にした場合であっても[横断検索](../../../users-guide/common/crosssearch.md)では検索結果に表示されます。これを防ぐために[横断検索](../../../users-guide/common/crosssearch.md)で検索できないようにオンに設定します。システム全体の横断検索を無効化したい場合、[Search.json](../../../setup/parameters/search-json.md)の「DisableCrossSearch」で変更可能です。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 既定値

既定値はオフです。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.4.0 以降|機能追加|

## 関連情報

-   [テーブル機能](../../../users-guide/table/index.md)
-   [共通機能：横断検索](../../../users-guide/common/crosssearch.md)
-   [開発者ガイド：拡張機能：拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)
-   [FAQ：一覧表示するレコードを所属組織別に分けたい](../../../FAQ/grid/faq-extended-sql-selecting-where.md)
-   [開発者ガイド：サーバスクリプト](../../../developers-guide/server-script/index.md)
-   [開発者ガイド：サーバスクリプト：view.Filters](../../../developers-guide/server-script/view/server-script-view-filters.md)
-   [レコードのアクセス制御（レコードの編集）](../../../users-guide/access-control/table-record-access-control.md)
-   [パラメータ設定：Search.json](../../../setup/parameters/search-json.md)
