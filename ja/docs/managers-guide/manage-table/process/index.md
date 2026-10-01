---
title: プロセス
category: プロセス
order: '100'
status: ''
parts: ''
urlstring: process
translationKey: process
shortname: プロセス
created: 2022-02-22
updated: 2026-02-10
---

## 概要

[プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)機能を使うことで、稟議申請などで用いられる承認ワークフロー機能を実現します。プロセス管理用のボタン設定、入力検証、ステータスごとの条件、ボタン表示有無のアクセス制御、自動採番、ボタン押下時の通知を設定することができます。  

具体的な使用方法については以下を参照してください。

-   [FAQ：稟議申請などのワークフロー（承認プロセス）をプロセス機能で実現する](../../../FAQ/sample-codes/faq-process-workflow.md)
-   [応用編：プロセスと状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [テーブルの管理：状況による制御](../control-by-status/index.md)

## 前提条件

-   この操作を実行するユーザは、サイトの管理権限が必要です。

## 操作手順

### プロセス設定画面を呼び出す

1.  プロセスを設定したいテーブルを開きます。
1.  ナビゲーションメニューで「管理」-[テーブルの管理](../index.md)をクリックします。

    ![ナビゲーションメニューの「管理」から「テーブルの管理」を選ぶところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/d68d842f207e4feda645bbadb9e7896c.png)

1.  [プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)タブをクリックします。

    ![テーブルの管理の「プロセス」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/910b057c061246079583c0acf8b5fef8.png)

### プロセスを設定する

プロセス管理は様々な機能を備えています。詳細は下記を参照してください。

-   [テーブルの管理：プロセス管理：共通設定・全般タブ](process-general.md)
-   [テーブルの管理：プロセス管理：入力検証タブ](process-input-validation.md)
-   [テーブルの管理：プロセス管理：条件タブ](process-conditions.md)
-   [テーブルの管理：プロセス管理：アクセス制御タブ](process-access-controls.md)
-   [テーブルの管理：プロセス管理：データの変更タブ](process-data-changes.md)
-   [テーブルの管理：プロセス管理：自動採番タブ](process-auto-numbering.md)
-   [テーブルの管理：プロセス管理：通知タブ](process-notifications.md)

![プロセス管理の設定画面。全般や入力検証などのタブが並ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/f01b4b9e4b4d45679e574d9287a2b88a.png)

### プロセス実行中の操作

プロセスを設定することで、レコードのフッターにボタンが追加されます。

![プロセスで追加されたボタンが並ぶレコードのフッター](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/2d3d85d7d4fd48fb836965fcd5c05925.png)

ボタンをクリックすると、プロセス設定に従い処理されます。

## 制限事項

-   「一括処理を許可」をチェックONにしても[入力必須](../editor/editor-settings/advanced-settings/general/table-management-required.md)以外の[入力検証](../editor/editor-settings/advanced-settings/input-validation/index.md)を指定している場合、一括処理は利用できません。
-   実行種別が「作成または更新ボタン」を選択した場合、[入力検証](../editor/editor-settings/advanced-settings/input-validation/index.md)は機能しません。
-   OnClickにスクリプトを設定する場合、「アクション種別」の「保存」、「ポストバック」は機能しません。
-   [一覧のヘッダメニューでフィルタを使用する](../filter/table-management-filter-use-grid-header-filters.md)を有効化している場合、[プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)の一括処理用の画面上で、ヘッダにマウスオーバーすると[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)項目が表示されますが、フィルタとして機能しません。

## 対応バージョン

| 対応バージョン | 内容                                                                             |
| :------------- | :------------------------------------------------------------------------------- |
| 1.4.10.0 以降  | 変更種別に値の関数操作を追加<br>メール通知の宛先にCc、Bccを追加                  |
| 1.4.11.0 以降  | 実行種別に追加したボタン／作成・更新を追加<br>共通設定・全般タブにアイコンを追加 |

## 関連情報

-   [応用編：プロセスと状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [FAQ：稟議申請などのワークフロー（承認プロセス）をプロセス機能で実現する](../../../FAQ/sample-codes/faq-process-workflow.md)
-   [テーブルの管理：状況による制御](../control-by-status/index.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：プロセス管理：共通設定・全般タブ](process-general.md)
-   [テーブルの管理：プロセス管理：入力検証タブ](process-input-validation.md)
-   [テーブルの管理：プロセス管理：条件タブ](process-conditions.md)
-   [テーブルの管理：プロセス管理：アクセス制御タブ](process-access-controls.md)
-   [テーブルの管理：プロセス管理：データの変更タブ](process-data-changes.md)
-   [テーブルの管理：プロセス管理：自動採番タブ](process-auto-numbering.md)
-   [テーブルの管理：プロセス管理：通知タブ](process-notifications.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力必須](../editor/editor-settings/advanced-settings/general/table-management-required.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力検証](../editor/editor-settings/advanced-settings/input-validation/index.md)
-   [テーブルの管理：フィルタ：一覧のヘッダメニューでフィルタを使用する](../filter/table-management-filter-use-grid-header-filters.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
