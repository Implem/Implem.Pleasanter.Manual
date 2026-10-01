---
title: レコードのアクセス制御（テーブルの管理）
category: アクセス制御
order: '600'
status: ''
parts: ''
urlstring: table-management-record-access-control
translationKey: table-management-record-access-control
shortname: アクセス制御
created: 2019-04-30
updated: 2026-06-15
---

## 概要

「レコード」の作成時と更新時に[レコードのアクセス制御](../../../users-guide/access-control/table-record-access-control.md)を自動的に設定することが可能です。

## 制限事項

1.  この設定はレコードの作成時と更新時に動作します。既存のレコードの「アクセス権」は変更されません。

## 前提条件

1.  「サイトの管理権限」と「権限の管理権限」が必要です。

## 操作手順

1.  対象の[テーブル](../../../users-guide/table/index.md)に移動してください。
1.  「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1.  [レコードのアクセス制御](../../../users-guide/access-control/table-record-access-control.md)タブを開いてください。
1.  選択肢一覧から[組織](../../department-administration/index.md)、[グループ](../../group-administration/index.md)、[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)、「管理者」、「担当者」、任意の[分類](../editor/editor-settings/columns/table-management-class.md)項目を選択し「有効化」ボタンをクリックしてください（エディタの詳細設定の選択肢一覧に[[Depts]],[[Groups]],[[Users]]が設定されている分類項目のみがレコードのアクセス制御の選択肢として表示されます）。
1.  「詳細設定」ボタンをクリックし必用な権限にチェックして「変更」ボタンをクリックしてください。
1.  「現在の設定」に不要な設定がある場合にはクリックして「権限削除」ボタンをクリックしてください。
1.  画面下部の「更新」ボタンをクリックしてください。

## 設定内容

| No  | 選択肢        | 説明                                                                                                                                                                                                                                                                                                                                                                      |
| :-- | :------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | [組織]        | 「レコード」を作成・更新した[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)が所属する[組織](../../department-administration/index.md)に指定した「アクセス権」が付与されます。                                                                                                                             |
| 2   | [グループ]    | 「レコード」を作成・更新した[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)が所属する[グループ](../../group-administration/index.md)に指定した「アクセス権」が付与されます。                                                                                                                             |
| 3   | [ユーザ]      | 「レコード」を作成・更新した[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)に指定した「アクセス権」が付与されます。                                                                                                                                                                                      |
| 4   | [項目] 管理者 | 新規作成・更新する「レコード」の[管理者項目](../editor/editor-settings/columns/table-management-manager.md)に指定した[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)に「アクセス権」が付与されます。                                                                                                     |
| 5   | [項目] 担当者 | 新規作成・更新する「レコード」の[担当者項目](../editor/editor-settings/columns/table-management-owner.md)に指定した[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)に「アクセス権」が付与されます。                                                                                                       |
| 6   | [項目] 分類   | 新規作成・更新する「レコード」の[分類項目](../editor/editor-settings/columns/table-management-class.md)に指定した任意の[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)、[組織](../../department-administration/index.md)、[グループ](../../group-administration/index.md)に「アクセス権」が付与されます。 |

## 対応バージョン

| 対応バージョン | 内容                                   |
| :------------- | :------------------------------------- |
| 1.3.17.0 以降  | レコード更新時のアクセス制御機能を追加 |

## 関連情報

-   [レコードのアクセス制御（レコードの編集）](../../../users-guide/access-control/table-record-access-control.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [テーブルの管理](../index.md)
-   [組織管理機能](../../department-administration/index.md)
-   [グループ管理機能](../../group-administration/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [テーブルの管理：項目：分類](../editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：管理者](../editor/editor-settings/columns/table-management-manager.md)
-   [テーブルの管理：項目：担当者](../editor/editor-settings/columns/table-management-owner.md)
