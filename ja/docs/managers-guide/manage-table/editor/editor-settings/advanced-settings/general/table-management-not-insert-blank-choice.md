---
title: 選択肢にブランクを挿入しない
category: エディタ
order: '11300'
status: ''
parts: ''
urlstring: table-management-not-insert-blank-choice
translationKey: table-management-not-insert-blank-choice
shortname: 選択肢にブランクを挿入しない
created: 2022-06-17
updated: 2026-05-18
---

## 概要

分類項目の[選択肢一覧](option-list/index.md)にブランクを挿入しない設定です。

## 制限事項

1.  [分類項目](../../columns/table-management-class.md)でのみ使用可能です。
1.  検索ダイアログ（[検索機能を使う](table-management-use-search.md)にチェック）で表示する選択肢「(未選択)」を非表示にすることはできません。

## 操作手順

1.  「管理」メニューの「[テーブルの管理](../../../../index.md)」から「[エディタ](../../../index.md)」タブを開きます。
1.  本機能を使いたい「[分類](../../columns/table-management-class.md)」項目を有効化欄から選択して、「詳細設定」ボタンをクリックします。
1.  「詳細設定」画面で「選択肢にブランクを挿入しない」のチェックをオンにして、「変更」ボタンをクリックします。

    ![項目の詳細設定の「選択肢にブランクを挿入しない」チェックボックス](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/c1dcb70a55fb4963a8f98f57645246cb.png)

1.  「エディタ」画面に戻り、「更新」ボタンをクリックします。  

## 設定イメージ

本機能が有効になった分類項目は以下の通り、選択肢にブランクが挿入されません。  

=== "チェックがオフの場合"

    ![チェックがオフのときの分類項目の選択肢](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/4ae3485e47ec43aaadd1c8ce63e3d25f.png)

=== "チェックがオンの場合"

    ![チェックがオンのときの分類項目の選択肢](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/98a195c8163744b18bd640585e893d3f.png)

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.3.3.0 以降   | 機能追加 |

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](option-list/table-management-choices-text-depts.md)
-   [テーブルの管理：項目：分類](../../columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：検索機能を使う](table-management-use-search.md)
