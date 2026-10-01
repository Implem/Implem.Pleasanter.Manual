---
title: レコードの集計
category: テーブル機能
order: '54'
status: ''
parts: ''
urlstring: table-record-aggregation
translationKey: table-record-aggregation
shortname: 集計
created: 2019-04-30
updated: 2025-09-19
---

## 概要

[テーブル](../../index.md)のレコード件数、任意の[数値](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)項目の合計・平均などを集計し、[一覧](table-grid.md)画面などの集計領域に表示します。

![一覧画面の集計領域にレコードの件数や合計を表示する操作](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-analysis/assets/2103569eaa234b53ad300442f984f08d.gif)

### 集計の折りたたみ・展開

集計領域の左上にある×をクリックすると、集計領域が折りたたまれて表示します。  
もう一度クリックすると、元の状態に展開します。

### フィルタとの連携

[フィルタ](table-record-search.md)を使用すると、指定した条件を満たすデータで再集計します。

### 分類項目によるグループ化

[分類](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)項目と組み合わせると、グループ化して集計できます。グループ化した集計のラベルをクリックすると、その項目による[フィルタ](table-record-search.md)の適用・解除を行えます。

### 期限超過

[期限付きテーブル](../../index.md)では[期限超過](../../../../managers-guide/manage-table/filter/table-management-filter-use-overdue-filter.md)したレコードの件数が表示されます。「期限超過」をクリックすると、該当のレコードを検索できます。

## 制限事項

-   [複数選択](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)を有効化している[分類](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)項目による「グループ化」は行えません。

## 前提条件

-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)の[集計](../../../../managers-guide/manage-table/aggregations/index.md)タブで事前に設定が必要です。

## 関連情報

-   [テーブル機能](../../index.md)
-   [テーブル機能：レコードの一覧画面](table-grid.md)
-   [テーブル機能：レコードの検索（フィルタ）](table-record-search.md)
-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)
-   [テーブルの管理：フィルタ：期限超過フィルタを使用する](../../../../managers-guide/manage-table/filter/table-management-filter-use-overdue-filter.md)
-   [テーブルの管理：項目：数値](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：分類](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：集計](../../../../managers-guide/manage-table/aggregations/index.md)
