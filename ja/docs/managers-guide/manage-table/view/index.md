---
title: ビュー
category: ビュー
order: '1'
status: ''
parts: ''
urlstring: table-management-view
translationKey: managers-guide/manage-table/view
shortname: ビュー
created: 2019-12-05
updated: 2024-05-24
---

## 概要

[テーブルの管理](../index.md)の[ビュー](index.md)タブでは、ビューの新規作成や、作成したビューの管理を行えます。

### ビュー

ビューを使用すると、テーブルに保存したデータを変更することなく、データの見え方（＝ビュー）だけを変更できます。ユーザは[フィルタ](../../../users-guide/table/record-authoring/data-analysis/table-record-search.md)や[ソート](../../../users-guide/table/record-authoring/data-analysis/table-record-sort.md)、[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)に表示する[項目](../editor/editor-settings/columns/index.md)（列）を設定し、その見え方をビューとして保存できます。

![テーブルの管理のビュータブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/view/assets/aeb9b855a16f490d9edc43ea0c64ba2e.png)

### ビューの設定

ビューを新規に作成する場合は、[新規作成](table-management-create-view.md)ボタンをクリックしてください。  
既存のビューの設定を変更する場合は、[詳細設定](table-management-view-list.md)ボタンをクリックしてください。  
新規作成画面または詳細設定画面が開き、下表のタブが表示されます。

| タブ名         | 説明                                                                                                                                                                                   |
| :------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 一覧           | [表示項目の選択](table-management-view-list.md)<br>[フィルタと集計の設定](table-management-view-filter-totaling.md)<br>[コマンドボタンの設定](table-management-view-command-button.md) |
| フィルタ       | ビューに表示されるレコードの検索（[フィルタ](table-management-view-keep-filter.md)）の設定                                                                                             |
| ソータ         | ビューに表示されるレコードの並び替え（[ソート](table-management-view-keep-sorter.md)）の設定                                                                                           |
| エディタ       | レコードのエディタ画面に表示されるボタンの設定                                                                                                                                         |
| カレンダー     | ビューをカレンダー表示した場合の設定                                                                                                                                                   |
| クロス集計     | ビューをクロス集計表示した場合の設定                                                                                                                                                   |
| ガントチャート | ビューをガントチャート表示した場合の設定                                                                                                                                               |
| 時系列チャート | ビューを時系列チャート表示した場合の設定                                                                                                                                               |
| カンバン       | ビューをカンバン表示した場合の設定                                                                                                                                                     |
| アクセス制御   | ビューに対する[アクセス制御の設定](table-management-view-permissions.md)                                                                                                               |

### ビューの保存種別

ビューの保存種別を設定できます。

![ビューの「保存種別」を設定する欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/view/assets/d66e6abac031453b992f486a80daf09f.png)

| 保存種別   | 説明                                                                                                                                                                                                                                        |
| :--------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| セッション | 次の条件で保持されます。<br><br>1. プリザンターからログアウトするまで<br>2. 設定ファイル[Session.json](../../../setup/parameters/session-json.md)のパラメータ`RetentionPeriod`に設定した期限内<br>3. すべてのブラウザウィンドウを閉じるまで |
| ユーザ     | データベースに保存し、次回も適用されます。                                                                                                                                                                                                  |
| 保存しない | 常に初期状態で表示します。                                                                                                                                                                                                                  |

## 必要な権限

![サイトの管理権限](../../../assets/badge_manage_site.svg)

## 操作手順

1.  任意のテーブルを開いてください。
1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  [テーブルの管理](../index.md)をクリックしてください。
1.  「ビュー」タブをクリックしてください。

## 関連情報

-   [テーブルの管理](../index.md)
-   [テーブルの管理：ビュー：新規作成](table-management-create-view.md)
-   [テーブルの管理：ビュー：詳細設定：一覧タブ：一覧の設定](table-management-view-list.md)
-   [テーブルの管理：ビュー：詳細設定：一覧タブ：コマンドボタンの設定](table-management-view-command-button.md)
-   [テーブルの管理：ビュー：詳細設定：アクセス制御タブ](table-management-view-permissions.md)
