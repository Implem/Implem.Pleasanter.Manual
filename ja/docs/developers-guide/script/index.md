---
title: スクリプト
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script
translationKey: script
shortname: ''
created: 2019-04-30
updated: 2026-08-31
---

## 概要

標準機能では実現できないUI操作等をAjaxのPOSTリクエストで可能にするために、サイト毎に適用可能なJavaScriptを設定することができます。

下記にはその追加方法、権限に関する注意事項、現在利用できる関数の一覧を記載します。

## スクリプトの追加方法

(この操作は「サイトの管理権限」が必要です。)

1.  対象のテーブルを開きます。
1.  「管理」メニューから[テーブルの管理](../../managers-guide/manage-table/index.md)をクリックします。
1.  [スクリプト](../../managers-guide/manage-table/scripts/index.md)タブを開きます。
1.  「新規作成」ボタンをクリックします。
1.  下表の項目を入力/設定します。
1.  「追加」ボタンをクリックします。
1.  画面下部の「更新」ボタンをクリックします。

| 項目名     | 説明                               | 設定方法               |
| :--------- | :--------------------------------- | :--------------------- |
| タイトル   | スクリプトのタイトル               | 任意のタイトルを入力   |
| スクリプト | スクリプトの内容                   | 任意のスクリプトを入力 |
| 無効       | スクリプトを無効にする場合チェック | チェックボックスで設定 |
| 出力先     | 出力先の画面を選択                 | チェックボックスで設定 |

## スクリプトの権限に関する注意事項

スクリプトはログインユーザの権限で実行されます。実行にあたり特定のユーザやシステム管理者の権限が必要な場合、そのユーザのAPIキーを指定する必要があります。

## スクリプトの関数一覧

### サイト情報取得スクリプト

| No  | 関数名                                              | 説明                                     |
| :-: | :-------------------------------------------------- | :--------------------------------------- |
|  1  | [$p.tableName](get-site-info/script-table-name.md)  | テーブルタイプを取得する関数です。       |
|  2  | [$p.controller](get-site-info/script-controller.md) | コントローラータイプを取得する関数です。 |
|  3  | [$p.action](get-site-info/script-action.md)         | アクションタイプを取得する関数です。     |

### サイト情報更新スクリプト

| No  | 関数名                                   | 説明                                                  |
| :-: | :--------------------------------------- | :---------------------------------------------------- |
|  1  | [$p.set](update-site-info/script-set.md) | 画面上の値変更と$p.dataへの格納を同時に行う関数です。 |

### サイトメッセージスクリプト

| No  | 関数名                                                  | 説明                                             |
| :-: | :------------------------------------------------------ | :----------------------------------------------- |
|  1  | [$p.clearMessage](site-message/script-clear-message.md) | 画面下に表示されるメッセージを削除する関数です。 |
|  2  | [$p.setMessage](site-message/script-set-message.md)     | 画面下にメッセージを表示させる関数です。         |

### コマンド操作やユーザ・組織・グループ操作などのスクリプト

| No  | 関数名                                                                | 説明                                                           |
| :-: | :-------------------------------------------------------------------- | :------------------------------------------------------------- |
|  1  | [$p.apiUrl](script-api/script-api-url.md)                             | APIリクエストのURL値の取得を行う関数です。                     |
|  2  | [$p.apiGet](script-api/script-api-get.md)                             | レコードを取得する関数です。                                   |
|  3  | [$p.apiCreate](script-api/script-api-create.md)                       | レコードを作成する関数です。                                   |
|  4  | [$p.apiUpdate](script-api/script-api-update.md)                       | レコードを更新する関数です。                                   |
|  5  | [$p.apiUpsert](script-api/script-api-upsert.md)                       | レコードを追加または更新する関数です。                         |
|  6  | [$p.apiDelete](script-api/script-api-delete.md)                       | レコードを削除する関数です。                                   |
|  7  | [$p.apiBulkDelete](script-api/script-api-bulk-delete.md)              | レコードを一括削除する関数です。                               |
|  8  | [$p.apiGetSite](script-api/script-api-get-site.md)                    | サイト情報を取得する関数です。                                 |
|  9  | [$p.apiCreateSite](script-api/script-api-create-site.md)              | サイトを作成する関数です。                                     |
| 10  | [$p.apiUpdateSite](script-api/script-api-update-site.md)              | サイトを更新する関数です。                                     |
| 11  | [$p.apiDeleteSite](script-api/script-api-delete-site.md)              | サイトを削除する関数です。                                     |
| 12  | [$p.apiGetClosestSiteId](script-api/script-api-get-closest-siteid.md) | サイト名検索で該当サイトに最も近いサイトIDを取得する関数です。 |
| 13  | [$p.apiUsersCreate](script-api/script-api-users-create.md)            | ユーザ情報を作成する関数です。                                 |
| 14  | [$p.apiUsersGet](script-api/script-api-users-get.md)                  | ユーザ情報を取得する関数です。                                 |
| 15  | [$p.apiUsersUpdate](script-api/script-api-users-update.md)            | ユーザ情報を更新する関数です。                                 |
| 16  | [$p.apiUsersDelete](script-api/script-api-users-delete.md)            | ユーザ情報を削除する関数です。                                 |
| 17  | [$p.apiDeptsGet](script-api/script-api-depts-get.md)                  | 組織情報を取得する関数です。                                   |
| 18  | [$p.apiGroupsGet](script-api/script-api-groups-get.md)                | グループ情報を取得する関数です。                               |
| 19  | [$p.apiGroupsCreate](script-api/script-api-groups-create.md)          | グループ情報を作成する関数です。                               |
| 20  | [$p.apiGroupsUpdate](script-api/script-api-groups-update.md)          | グループ情報を更新する関数です。                               |
| 21  | [$p.apiGroupsDelete](script-api/script-api-groups-delete.md)          | グループ情報を削除する関数です。                               |
| 22  | [$p.apiSendMail](script-api/script-api-send-mail.md)                  | メールを送信する関数です。                                     |

### 値の設置/更新/取得/削除系スクリプト

| No  | 関数名                                                               | 説明                                                                                                                                           |
| :-: | :------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------- |
|  1  | [$p.id](value-operations/script-id.md)                               | レコードのid値を取得する関数です。                                                                                                             |
|  2  | [$p.siteId](value-operations/script-site-id.md)                      | サイトのId値を取得する関数です。                                                                                                               |
|  3  | [$p.loginId](value-operations/script-login-id.md)                    | ログインIdを取得する関数です。                                                                                                                 |
|  4  | [$p.userId](value-operations/script-user-id.md)                      | ログインしているユーザのユーザIdを取得する関数です。                                                                                           |
|  5  | [$p.userName](value-operations/script-user-name.md)                  | ログインしているユーザの名前を取得する関数です。                                                                                               |
|  6  | [$p.getColumnName](value-operations/script-get-column-name.md)       | 対象項目のカラム名（データベースの列名）を取得する関数です。                                                                                   |
|  7  | [$p.getControl](value-operations/script-get-control.md)              | 対象の項目名から要素を取得する関数です。                                                                                                       |
|  8  | [$p.getField](value-operations/script-get-field.md)                  | 対象の項目名からFieldを取得する関数です。                                                                                                      |
|  9  | [$p.getGridRow](value-operations/script-get-grid-row.md)             | [一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)にてレコードのtrタグ要素を取得する関数です。                   |
| 10  | [$p.getGridCell](value-operations/script-get-grid-cell.md)           | [一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)のtdタグの要素を取得する関数です。                             |
| 11  | [$p.getGridColumnIndex](value-operations/script-get-column-index.md) | [一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)にてレコードの表示名のデータが何列目にあるか取得する関数です。 |
| 12  | [$p.on](value-operations/script-on.md)                               | 各イベント発生時に任意の処理を実行することができる関数です。                                                                                     |

### イベント発火スクリプト

| No  | 関数名                                                                     | タイミング                         | 説明                                                                                                                                        |
| :-: | :------------------------------------------------------------------------- | :--------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------ |
|  1  | [$p.events.on_editor_load](events/script-events-on-editor-load.md)         | 編集画面を読み込んだ時             | 「編集画面」を読み込んだときに実行する関数です。                                                                                            |
|  2  | [$p.events.on_grid_load](events/script-events-on-grid-load.md)             | 一覧画面を読み込んだ時             | [一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)を読み込んだときに実行する関数です。                        |
|  3  | [$p.events.on_calendar_load](events/script-events-on-calendar-load.md)     | カレンダーを読み込んだ時           | [カレンダー](../../users-guide/dashboard/dashboard-calendar.md)を読み込んだときに実行する関数です。                                         |
|  4  | [$p.events.on_crosstab_load](events/script-events-on-crosstab-load.md)     | クロス集計を読み込んだ時           | [クロス集計](../../users-guide/table/record-authoring/data-visualize/table-crostab.md)を読み込んだときに実行する関数です。                  |
|  5  | [$p.events.on_gantt_load](events/script-events-on-gantt-load.md)           | ガントチャートを読み込んだ時       | [ガントチャート](../../users-guide/table/record-authoring/data-visualize/table-gantt-chart.md)を読み込んだときに実行する関数です。          |
|  6  | [$p.events.on_burndown_load](events/script-events-on-burndown-load.md)     | バーンダウンチャートを読み込んだ時 | [バーンダウンチャート](../../users-guide/table/record-authoring/data-visualize/table-burndown-chart.md)を読み込んだときに実行する関数です。 |
|  7  | [$p.events.on_timeseries_load](events/script-events-on-timeseries-load.md) | 時系列チャートを読み込んだ時       | [時系列チャート](../../managers-guide/manage-table/time-series-chart/index.md)を読み込んだときに実行する関数です。    |
|  8  | [$p.events.on_analy_load](events/script-events-on-analy-load.md)           | 分析チャートを読み込んだ時         | [分析チャート](../../users-guide/table/record-authoring/data-visualize/table-analy-chart.md)を読み込んだときに実行する関数です。            |
|  9  | [$p.events.on_kamban_load](events/script-events-on-kamban-load.md)         | カンバンを読み込んだ時             | [カンバン](../../users-guide/table/record-authoring/data-visualize/table-kanban-chart.md)を読み込んだときに実行する関数です。               |
| 10  | [$p.events.before_validate](events/script-events-before-validate.md)       | 入力値の検証前                     | バリデーションチェックを行う前に実行する関数です。                                                                                          |
| 11  | [$p.events.after_validate](events/script-events-after-validate.md)         | 入力値の検証後                     | バリデーションチェックを行った後に実行する関数です。                                                                                        |
| 12  | [$p.events.before_send](events/script-events-before-send.md)               | データ送信前                       | サーバへデータを送信する前に実行する関数です。                                                                                              |
| 13  | [$p.events.after_send](events/script-events-after-send.md)                 | データ送信後                       | サーバへデータを送信した後に実行する関数です。                                                                                              |
| 14  | [$p.events.before_set](events/script-events-before-set.md)                 | 画面の更新前                       | サーバへデータを送信後、画面内容を更新する前に実行する関数です。                                                                            |
| 15  | [$p.events.after_set](events/script-events-after-set.md)                   | 画面の更新後                       | サーバへデータを送信後、画面内容を更新した後に実行する関数です。                                                                            |

## 関連情報

[テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
