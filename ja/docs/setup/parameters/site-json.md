---
title: Site.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: site-json
translationKey: site-json
shortname: Site.json
created: 2019-10-29
updated: 2026-09-08
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|TopOrderBy|123|トップ画面におけるサイトの並び替えを、特定のユーザのみが行えるように制限します。 「ユーザーID」または「0」を指定します。「ユーザーID」を指定した場合、そのユーザおよび[特権ユーザ](../../managers-guide/user-administration/user-management-privileged-users.md)のみがトップ画面の並び替えを実施できます。「0」を指定した場合、すべてのユーザでトップ画面の並び替えが実施可能となります。トップ以外のフォルダで並び替えを抑制する場合は[サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)で「サイトの管理」権限を外してください。|
|DisableSiteConditions|true|サイト情報の表示有無を指定します。 ※1 ※2|
|SimpleMode|設定方法は後述|シンプルモードを設定します。|

※1 本パラメータはプリザンターの全サイトの表示に影響します。trueを設定すると、サイト単位で指定している「サイト機能：サイト設定の閲覧と変更」の「サイト情報を表示しない」の設定にかかわらず、全サイト情報が非表示になります。
※2 trueを設定した場合に非表示になるサイト情報は「最終更新からの経過時間」「件数」「超過件数」です。サイト種別を示すアイコンはtrueの場合にも表示します。詳細は「[サイト機能：サイト情報の表示の切り替え](../../users-guide/site/site-information.md)」を参照してください。

## SimpleMode

シンプルモードは、サイト（[フォルダ](../../users-guide/folder/index.md)、[テーブル](../../users-guide/table/index.md)、[Wiki](../../users-guide/wiki/index.md)、[ダッシュボード](../../users-guide/dashboard/dashboard-add-parts.md)）の管理画面で利用頻度の高いタブのみを表示する機能です。シンプルモードの設定内容は以下の通りです。

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Enabled|false|trueに設定することでシンプルモードを有効にします。|
|Default|true|trueに設定した場合、テーブルの管理画面表示時の初期状態がシンプルモードになります。|
|DisplaySwitch|true|trueに設定した場合、シンプルモードと通常のタブ表示とを切り替えるためのボタンが表示されます。|
|Tabs|["General", "Grid", "Filters", "DashboardParts", "Editor", "SiteAccessControl"]|シンプルモード時に表示するタブを配列形式で指定します。|

### Tabsに指定可能なタブ名の一覧

|タブ名|タブの表示名|
|--|--|
|General|全般|
|Guide|ガイド|
|SiteImageSettingsEditor|サイト画像|
|Styles|スタイル|
|Scripts|スクリプト|
|Html|HTML|
|DashboardParts|ダッシュボードパーツ|
|DataView|ビュー|
|Notifications|通知|
|Mail|メール|
|Publish|公開|
|Grid|一覧|
|Filters|フィルタ|
|Aggregations|集計|
|Editor|エディタ|
|Links|リンク|
|Histories|履歴|
|Move|移動|
|Summaries|サマリ|
|Formulas|計算式|
|Processes|プロセス|
|StatusControls|状況による制御|
|Reminders|リマインダー|
|Import|インポート|
|Export|エクスポート|
|Calendar|カレンダー|
|Crosstab|クロス集計|
|Gantt|ガントチャート|
|BurnDown|バーンダウンチャート|
|TimeSeries|時系列チャート|
|Analy|分析チャート|
|Kanban|カンバン|
|ImageLib|画像ライブラリ|
|Search|検索|
|SiteIntegration|サイト統合|
|ServerScript|サーバスクリプト|
|SiteAccessControl|サイトのアクセス制御|
|RecordAccessControl|レコードのアクセス制御|
|ColumnAccessControl|項目のアクセス制御|
|ChangeHistoryList|変更履歴の一覧|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.14.0 以降|DisableSiteConditionsを追加|
|1.4.15.0以降|SimpleModeを追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [ユーザ管理機能：特権ユーザの設定](../../managers-guide/user-administration/user-management-privileged-users.md)
-   [サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)
-   [フォルダ機能](../../users-guide/folder/index.md)
-   [テーブル機能](../../users-guide/table/index.md)
-   [Wiki機能](../../users-guide/wiki/index.md)
-   [ダッシュボード機能：パーツの追加](../../users-guide/dashboard/dashboard-add-parts.md)
