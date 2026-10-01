---
title: 状況による制御
category: 状況による制御
order: '3'
status: ''
parts: ''
urlstring: status-control
translationKey: status-control
shortname: 状況による制御
created: 2022-07-04
updated: 2026-01-13
---

## 概要

[状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)機能を使うことで、ステータスに応じたレコード単位の読取専用および項目単位の[入力必須](../editor/editor-settings/advanced-settings/general/table-management-required.md)、[読取専用](../editor/editor-settings/advanced-settings/general/table-management-readonly.md)、[非表示](../editor/editor-settings/advanced-settings/general/table-management-hide.md)を設定します。また、[状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)を有効とする[条件](../../../FAQ/editor/faq-condition-mode-range.md)や[アクセス制御](../site-access-control/index.md)を設定することができます。

## 制限事項

1.  [状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)機能の[非表示](../editor/editor-settings/advanced-settings/general/table-management-hide.md)設定はUIにおける表示をなくすもので、HTML上には対象の項目が存在します。項目をHTML上からもなくしたい場合は[項目のアクセス制御](../column-access-control/index.md)をご利用ください。
1.  [インポート](../../../users-guide/table/record-authoring/create-records/table-record-import.md)、[一括更新](../../../users-guide/table/record-authoring/edit-records/table-record-bulkupdate.md)やAPIでのデータ登録・更新時は[状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)機能での読取専用や入力必須の設定は無視されます。
1.  レコードの[カレンダー](../../../users-guide/dashboard/dashboard-calendar.md)表示、[カンバン](../../../users-guide/table/record-authoring/data-visualize/table-kanban-chart.md)表示でのドラッグ＆ドロップによるデータ更新時は[状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)機能での読取専用の設定は無視されます。
1.  本機能の設定には、サイトの管理権限が必要です。

## 設定手順

1.  該当のテーブルを開いた状態でナビゲーションメニューより「管理」－[テーブルの管理](../index.md)をクリックしてください。  

       ![「管理」メニューを開いたナビゲーションメニュー。「テーブルの管理」が並ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/control-by-status/assets/976b9bf498394c90b566ba17361133f4.png)

1.  テーブルの管理から[状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)タブをクリックして開きます。

       ![テーブルの管理の「状況による制御」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/control-by-status/assets/cadc676dedca44eaaa0c92c1a3e46061.png)

## 設定内容

「新規作成」ボタンをクリックし、[状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)を設定します。

### 詳細設定：全般タブ

![状況による制御の詳細設定の「全般」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/control-by-status/assets/04958ba3f8194254aba4005a72898445.png)

#### 詳細設定

| 項目名 | 説明                                                                                                                                      |
| :----- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| 名称   | 任意の名称を設定します。                                                                                                                  |
| 状況   | [状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)の対象とするステータスを設定します。 [^1]          |
| 説明   | 任意の説明を設定します。                                                                                                                  |
| 無効   | [状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)を一時的に動作させない場合にチェックしてください。 |

[^1]:　ステータスに応じて、[状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)の設定が有効になります。また、*を指定することで、全てのステータスで有効になります。

#### レコードの制御

レコードを読取専用にする場合はチェックをオンにします。

#### 項目の制御

各項目について[入力必須](../editor/editor-settings/advanced-settings/general/table-management-required.md)、[読取専用](../editor/editor-settings/advanced-settings/general/table-management-readonly.md)、[非表示](../editor/editor-settings/advanced-settings/general/table-management-hide.md)を設定します。

| ボタン   | 説明                                                                                                                                                                                                                                                                                                                         |
| :------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 無し     | 対象の項目について[入力必須](../editor/editor-settings/advanced-settings/general/table-management-required.md)、[読取専用](../editor/editor-settings/advanced-settings/general/table-management-readonly.md)、[非表示](../editor/editor-settings/advanced-settings/general/table-management-hide.md)の設定をリセットします。 |
| 入力必須 | [状況](../editor/editor-settings/columns/table-management-status.md)で設定したステータスに該当する場合、対象の項目が[入力必須](../editor/editor-settings/advanced-settings/general/table-management-required.md)になります。                                                                                                 |
| 読取専用 | [状況](../editor/editor-settings/columns/table-management-status.md)で設定したステータスに該当する場合、対象の項目が[読取専用](../editor/editor-settings/advanced-settings/general/table-management-readonly.md)になります。                                                                                                 |
| 非表示   | [状況](../editor/editor-settings/columns/table-management-status.md)で設定したステータスに該当する場合、対象の項目が[非表示](../editor/editor-settings/advanced-settings/general/table-management-hide.md)になります。                                                                                                       |

### 詳細設定：条件タブ

[状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)を有効にする条件を設定します。

![状況による制御の詳細設定の「条件」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/control-by-status/assets/367d98cf0c3f43eeb72ee8a3899b67b9.png)

項目のプルダウンから対象項目を選択、追加して条件を設定します。

### 詳細設定：アクセス制御タブ

[状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)を有効にする[組織](../../department-administration/index.md)、[グループ](../../group-administration/index.md)、[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)を設定します。

![状況による制御の詳細設定の「アクセス制御」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/control-by-status/assets/e57548dae17f4ecdb0d85f838b08c9e5.png)

選択肢一覧より、対象とするユーザ/組織/グループを選択して追加します。

## 設定例

[状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)の活用例については以下のFAQを参照してください。
[FAQ：項目の非表示や読取専用などの状態変更を状況による制御機能で実現する](../../../FAQ/sample-codes/faq-status-control-workflow.md)

## 対応バージョン

| 対応バージョン | 内容                                |
| :------------- | :---------------------------------- |
| 1.3.12.0 以降  | 機能追加                            |
| 1.3.13.0 以降  | 状況項目での*(全ての状況)指定に対応 |
| 1.5.0.0 以降   | 「無効」オプションを追加            |

## 関連情報

-   [応用編：プロセスと状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力必須](../editor/editor-settings/advanced-settings/general/table-management-required.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../editor/editor-settings/advanced-settings/general/table-management-readonly.md)
-   [テーブルの管理：エディタ：項目の詳細設定：非表示](../editor/editor-settings/advanced-settings/general/table-management-hide.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
-   [サイトのアクセス制御](../site-access-control/index.md)
-   [項目のアクセス制御](../column-access-control/index.md)
-   [組織管理機能：インポート](../../department-administration/dept-import.md)
-   [テーブル機能：レコードの一括更新](../../../users-guide/table/record-authoring/edit-records/table-record-bulkupdate.md)
-   [ダッシュボード機能：パーツの追加：カレンダー](../../../users-guide/dashboard/dashboard-calendar.md)
-   [テーブル機能：レコードのカンバン表示](../../../users-guide/table/record-authoring/data-visualize/table-kanban-chart.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：項目：状況](../editor/editor-settings/columns/table-management-status.md)
-   [組織管理機能](../../department-administration/index.md)
-   [グループ管理機能](../../group-administration/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [FAQ：項目の非表示や読取専用などの状態変更を「状況による制御」機能で実現する](../../../FAQ/sample-codes/faq-status-control-workflow.md)
