---
title: レコードのアクセス制御（レコードの編集）
category: アクセス制御
order: '700'
status: ''
parts: ''
urlstring: table-record-access-control
translationKey: table-record-access-control
shortname: レコードのアクセス制御
created: 2021-05-22
updated: 2026-06-15
---

## 概要

[テーブル](../table/index.md)の「レコード」に「アクセス権」を設定することができます。[サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)で「アクセス権」を割り当てられていない[ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)にも特定のレコードに対してのみ「アクセス権」を付与することができます。[サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)と「レコードのアクセス制御」を同時に設定した場合には、両方の「アクセス権」が有効になります。例えば[サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)で「読み取り権限」を付与し「レコードのアクセス制御」で「更新権限」を付与した場合には、「読み取り権限」と「更新権限」の両方が有効になります。

## 制限事項

1. 「レコードのアクセス制御」では「レコード」1件1件に権限の設定を行う必要があります。特定の条件で一覧画面に表示するレコードを絞り込みたいケースでは[サーバスクリプト](../../developers-guide/server-script/index.md)の「view.Filtersオブジェクト」または[拡張SQL](../../developers-guide/extended-features/extended-sql/index.md)の[OnSelectingWhere](../../FAQ/grid/faq-extended-sql-selecting-where.md)を使用してください。
1. 「レコードのアクセス制御」で「作成権限」にチェックできますが、作成権限は付与されません。[サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)で設定してください。
1. 「レコードのアクセス制御」で「エクスポート権限」にチェックできますが、エクスポート権限は付与されません。[サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)で設定してください。
1. 「レコードのアクセス制御」で「インポート権限」にチェックできますが、インポート権限は付与されません。[サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)で設定してください。
1. 「レコードのアクセス制御」で「サイトの管理権限」にチェックできますが、サイトの管理権限は付与されません。[サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)で設定してください。

## 前提条件

1. 「レコード」の「読み取り権限」、「更新権限」、「権限の管理権限」が必要です。

## 操作手順

1. 対象のテーブルに移動してください。
1. [一覧画面](../table/record-authoring/data-analysis/table-grid.md)から対象のレコードを検索してください。
1. 対象のレコードをクリックしてください。
1. [エディタ](../table/record-authoring/edit-records/table-editor.md)が表示されるので「レコードのアクセス制御」タブを開いてください。
1. 選択肢一覧から対象となる[組織](../../managers-guide/department-administration/index.md)、[グループ](../../managers-guide/group-administration/index.md)、[ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)を選択し「権限追加」ボタンをクリックしてください。
1. 「詳細設定」ボタンをクリックし必用な権限にチェックして「変更」ボタンをクリックしてください。
1. 「権限設定の一覧」に不要な設定がある場合にはクリックして「権限削除」ボタンをクリックしてください。
1. 「更新」ボタンをクリックしてください。
1. 「"xxxx"を更新しました。」と表示されれば完了です。xxxxにはレコードのタイトルが表示されます。

## 詳細情報

1. 「レコード」作成時に自動的に「レコードのアクセス制御」を設定することができます。設定方法は「[レコードのアクセス制御（テーブルの管理）](../../managers-guide/manage-table/record-access-control/index.md)」を参照してください。

## 関連情報

-   [テーブル機能](../table/index.md)
-   [サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
-   [開発者ガイド：拡張機能：拡張SQL](../../developers-guide/extended-features/extended-sql/index.md)
-   [FAQ：一覧表示するレコードを所属組織別に分けたい](../../FAQ/grid/faq-extended-sql-selecting-where.md)
-   [テーブル機能：レコードの一覧画面](../table/record-authoring/data-analysis/table-grid.md)
-   [テーブル機能：レコードのエディタ画面](../table/record-authoring/edit-records/table-editor.md)
-   [組織管理機能](../../managers-guide/department-administration/index.md)
-   [グループ管理機能](../../managers-guide/group-administration/index.md)
-   [レコードのアクセス制御（テーブルの管理）](../../managers-guide/manage-table/record-access-control/index.md)