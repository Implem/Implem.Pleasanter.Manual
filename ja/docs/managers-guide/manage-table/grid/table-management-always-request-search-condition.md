---
title: 常に検索条件を要求する
category: 一覧画面
order: '280'
status: ''
parts: ''
urlstring: table-management-always-request-search-condition
translationKey: table-management-always-request-search-condition
shortname: 常に検索条件を要求する
created: 2021-05-06
updated: 2025-08-13
---

## 概要

「常に検索条件を要求する」をオンにすると[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)の条件指定を1つ以上行わないと「レコード」を表示しない動作になります。必ず「検索条件」の入力を求める場合にオンにします。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。
1. 本機能を有効にしても[サーバスクリプト](../../../developers-guide/server-script/index.md)の[view.Filters](../../../developers-guide/server-script/view/server-script-view-filters.md)を設定した場合は、一覧画面等の表示時にview.Filterに指定した条件で抽出したレコードが表示されます。

## 操作手順

1. 対象の[テーブル](../../../users-guide/table/index.md)を開いてください。
1. 「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1. [一覧](index.md)タブを開いてください。
1. 画面下部にある「常に検索条件を要求する」のチェックボックスをオンにします。
1. 画面下部の「更新」ボタンをクリックしてください。

## 関連情報

-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [開発者ガイド：サーバスクリプト](../../../developers-guide/server-script/index.md)
-   [開発者ガイド：サーバスクリプト：view.Filters](../../../developers-guide/server-script/view/server-script-view-filters.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：一覧画面](index.md)