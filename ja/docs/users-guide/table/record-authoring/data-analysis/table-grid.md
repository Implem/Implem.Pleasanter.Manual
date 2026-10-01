---
title: レコードの一覧画面
category: テーブル機能
order: '11'
status: ''
parts: ''
urlstring: table-grid
translationKey: table-grid
shortname: 一覧画面
created: 2019-05-02
updated: 2025-10-21
---

## 概要

「一覧画面」を開くと、すぐにテーブルに格納されたレコードが一覧形式で表示されます。

### レコード一覧画面の構成と見方

![一覧画面の各部に番号を振った図](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-analysis/assets/dea7a81e22c140089ef245935bab6f94.png)

| No  | 名称                                      | 解説                                                                                                                |
| --: | :---------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| 1   | [ビュー](../../../hands-on/advanced/advanced-operations-view.md)選択 | 最初にテーブルを開いた際に表示する項目やソート、フィルタの初期状態を設定できます。                                  |
| 2   | [フィルタ](../../../hands-on/advanced/advanced-operations-link.md)   | レコードを絞り込むための条件を指定します。                                                                          |
| 3   | [集計](../../../../managers-guide/manage-table/aggregations/index.md)   | レコード件数、任意の数値項目の合計や平均等の集計結果を表示します。                                                  |
| 4   | [ソート](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md) | レコードを特定の項目について昇順・降順に並べ替えます。既定では保存された日時が新しい順に表示されます。              |
| 5   | [検索結果一覧](#Search-results-list)      | フィルタで指定した条件に合致するレコード（特に設定しなければすべてのレコード）が表示されます。                      |
| 6   | [一括移動](../edit-records/table-record-bulkmove.md)      | 選択したレコードをまとめて移動します。利用には[設定](../../../../managers-guide/manage-table/move/index.md)が必要です。                     |
| 7   | [一括削除](../edit-records/table-record-bulkdelete.md)    | 選択したレコードをまとめて削除します。                                                                              |
| 8   | [インポート](../create-records/table-record-import.md)              | CSVファイルを読み込む機能を使い、テーブルにレコードを一括追加します。                                               |
| 9   | [エクスポート](../../../../developers-guide/api/table-operations/api-export.md)             | CSVファイルを書き出す機能を使い、テーブルからレコードを書き出します。フィルタやソートを反映した状態で書き出せます。 |
| 10  | [一括更新](../edit-records/table-record-bulkupdate.md)    | 選択した項目の値をまとめて変更します。利用には[設定](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-bulk-update.md)が必要です。              |

なお、フィルタとソートは[ビューの保存種別](../../../dashboard/dashboard-view.md)の影響を受けます。

## 制限事項

1. [項目のアクセス制御](../../../../managers-guide/manage-table/column-access-control/index.md)で「読取り」権限を持たない列は表示できません。
1. 「子テーブル」の項目を一覧画面に表示している場合には、表の左端に表示される行選択のチェックボックスは表示されません。
1. 「更新権限」、「削除権限」、「エクスポート権限」のいずれも持たない場合は、表の左端に表示される行選択のチェックボックスは表示されません。
1.  バージョン1.4.20.0以降でサポートされた検索結果一覧のドラッグ操作は、[第1世代ユーザインターフェース](../../../../managers-guide/user-administration/user-management-theme.md)では非対応です。

## 前提条件

1. レコードを表示するには[サイト](../../../site/index.md)またはレコードの「読取り権限」が必要です。
1. [集計](../../../../managers-guide/manage-table/aggregations/index.md)を使用するには[テーブルの管理](../../../../managers-guide/manage-table/index.md)を使用して有効化する必要があります。
1. [ビュー](../../../hands-on/advanced/advanced-operations-view.md)を使用するには[テーブルの管理](../../../../managers-guide/manage-table/index.md)を使用して有効化する必要があります。
1. [一括移動](../edit-records/table-record-bulkmove.md)を使用するには[テーブルの管理](../../../../managers-guide/manage-table/index.md)を使用して有効化する必要があります。
1. [一覧編集](../edit-records/table-record-editongrid.md)を使用するには[テーブルの管理](../../../../managers-guide/manage-table/index.md)を使用して有効化する必要があります。

## 検索結果一覧の文字列選択について

**検索結果一覧で ++alt++ キー（macOSの場合は ++option++ キー）を押しながらドラッグすると、文字列を選択できます**。

<span class="pl-attention">Windowsでウィンドウの切り替えに ++alt+tab++ のショートカットを使っていて、意図せず文字列が選択されてしまう場合には、++alt++ キーを押してください。</span>

<a id="Search-results-list"></a>

## 検索結果一覧について

検索結果一覧に表示されるレコード数は[ページ当たりの表示件数](../../../../managers-guide/manage-table/grid/table-management-grid-page-size.md)で指定した数となります。画面を下にスクロールすると、次のレコードが同じ数だけ読み込まれ、表示されます。

[第2世代ユーザインターフェース](../../../../managers-guide/user-administration/user-management-theme.md)を利用していれば、バージョン1.4.20.0以降、ドラッグ操作により検索結果一覧を上下左右、自由に移動できます。詳細は[一覧表示UIのスクロール操作](../../../common/common-func-scrolling-operation-on-grids.md)をご覧ください。

![検索結果一覧をドラッグして上下左右に動かす操作のアニメーション](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-analysis/assets/c17f871a72f3429b81a996f6019a9481.gif)

### 検索結果一覧の表示に関わる設定項目

[一覧画面の項目の詳細設定](../../../../managers-guide/manage-table/grid/advanced-settings/index.md)では、検索結果一覧の表示方法を細かく制御できます。

### セルの横幅

項目の表示幅をピクセル（px）単位で指定できます。特定の項目の表示において、表示が省略されてしまう、行が折れてしまうといった状況を回避できます。詳細は[セルの横幅](../../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)をご覧ください。

??? tip "利用イメージ"

    以下の図では、検索結果一覧のタイトル/内容項目の幅を400pxに設定することで、タイトル全体を確認できています。

    ![セルの横幅の利用イメージ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-analysis/assets/15c847277c68476ba96f902daa30b04a.png)

### 左端でスクロール固定

特定の項目（列）を表示させたまま、ドラッグでスクロールできます（以下の利用イメージを参照）。詳細は[左端でスクロール固定](../../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-sticky-on-left-edge.md)をご覧ください。

??? tip "利用イメージ"

    複数の項目を固定することができます。以下の図では、作業工程項目とタイトル/内容項目を左端でスクロール固定させています。

    ![左端でスクロール固定の利用イメージ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-analysis/assets/e08625b8dbd043c38fa0e8d9d13f65a0.gif)

### その他の設定項目

上記2つ以外にも、以下のような設定項目があります。

1. [表示名](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)
1. [一覧の書式](../../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-format.md)
1. [セルCSS](../../../../FAQ/grid/faq-grid-cell-color-by-num-range.md)
1. [左端でスクロール固定](../../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-sticky-on-left-edge.md)
1. [セルの横幅](../../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)
1. [カスタムデザインを使用](../../../../managers-guide/manage-table/grid/advanced-settings/table-management-use-grid-design.md)

## 対応バージョン

| 対応バージョン | 内容                                                                                                   |
| -------------- | ------------------------------------------------------------------------------------------------------ |
| 1.4.20.0以降   | ・検索結果一覧のドラッグ操作を追加<br>・新規カスタマイズ項目（セルの横幅・左端でスクロール固定）を追加 |

## 関連情報

-   [応用編：ビュー](../../../hands-on/advanced/advanced-operations-view.md)
-   [応用編：リンク](../../../hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：集計](../../../../managers-guide/manage-table/aggregations/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)
-   [テーブル機能：レコードの一括移動](../edit-records/table-record-bulkmove.md)
-   [テーブルの管理：移動](../../../../managers-guide/manage-table/move/index.md)
-   [テーブル機能：レコードの一括削除](../edit-records/table-record-bulkdelete.md)
-   [組織管理機能：インポート](../../../../managers-guide/department-administration/dept-import.md)
-   [開発者ガイド：API：テーブル操作：テーブルのエクスポート](../../../../developers-guide/api/table-operations/api-export.md)
-   [テーブル機能：レコードの一括更新](../edit-records/table-record-bulkupdate.md)
-   [テーブルの管理：エディタ：項目の詳細設定：一括更新を許可](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-bulk-update.md)
-   [ダッシュボード機能：ビューの保存種別](../../../dashboard/dashboard-view.md)
-   [テーブルの管理：一覧画面：ページ当たりの表示件数](../../../../managers-guide/manage-table/grid/table-management-grid-page-size.md)
-   [共通機能：一覧表示UIのスクロール操作](../../../common/common-func-scrolling-operation-on-grids.md)
-   [テーブルの管理：一覧画面：項目の詳細設定](../../../../managers-guide/manage-table/grid/advanced-settings/index.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：セルの横幅](../../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：左端でスクロール固定](../../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-sticky-on-left-edge.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：一覧の書式](../../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-format.md)
-   [FAQ：一覧画面で数値の範囲によってセルの色を変えたい](../../../../FAQ/grid/faq-grid-cell-color-by-num-range.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：カスタムデザインを使用](../../../../managers-guide/manage-table/grid/advanced-settings/table-management-use-grid-design.md)
-   [項目のアクセス制御](../../../../managers-guide/manage-table/column-access-control/index.md)
-   [第1世代ユーザインターフェース](../../../../managers-guide/user-administration/user-management-theme.md)
-   [サイト機能](../../../site/index.md)
-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードの一覧編集](../edit-records/table-record-editongrid.md)
