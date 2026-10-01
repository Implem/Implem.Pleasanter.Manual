---
title: 既定のビュー
category: 一覧画面
order: '250'
status: ''
parts: ''
urlstring: table-management-default-view
translationKey: table-management-default-view
shortname: 既定のビュー
created: 2021-05-06
updated: 2025-01-30
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)の「既定のビュー」を設定します。「既定のビュー」を使用するとログイン後に最初にテーブルを開いた際に表示する[項目](../editor/editor-settings/columns/index.md)や一覧表の[ソート](../editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)や[並び替え](../../../users-guide/table/record-authoring/data-analysis/table-record-sort.md)等の初期状態をセットすることができます。

## 制限事項

1. 既定のビューは[組織](../../department-administration/index.md)毎や[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)毎に変更することはできません。既定のビューを動的に切り替える場合には[サーバスクリプト](../../../developers-guide/server-script/index.md)の「siteSettingsオブジェクト」の「DefaultViewId」を使用してください。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。
1. [ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)が1つ以上作成されていることが必要です。

ビューを設定済みの場合のみ「既定のビュー」の選択肢が表示されます。
![ビューを設定済みのとき、一覧タブに「既定のビュー」の選択肢が出た状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/54f4cca37282485ea7dd91a8d75dffad.png)

ビューを設定していない場合「既定のビュー」は表示されません。  
![ビューを設定していないとき、一覧タブに「既定のビュー」が出ない状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/e66ae8fb84b84a52a8f1fed4dd94dfa7.png)

## 操作手順

1. 対象の[テーブル](../../../users-guide/table/index.md)を開いてください。
1. 「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1. [一覧](index.md)タブを開いてください。
1. 画面下部にある「既定のビュー」のセレクトボックスから任意の設定を選択してください。
1. 画面下部の「更新」ボタンをクリックしてください。

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理：項目](../editor/editor-settings/columns/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](../editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)
-   [テーブル機能：レコードの並び替え（ソート）](../../../users-guide/table/record-authoring/data-analysis/table-record-sort.md)
-   [組織管理機能](../../department-administration/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [開発者ガイド：サーバスクリプト](../../../developers-guide/server-script/index.md)
-   [応用編：ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：一覧画面](index.md)