---
title: サーバスクリプトで期限付きテーブルの完了項目の値を取得すると1日プラスされた日付が取得される
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-get-completiontime-using-server-script
translationKey: faq-get-completiontime-using-server-script
shortname: ''
created: 2025-06-11
updated: 2025-06-19
---

## 回答

仕様です。[完了項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)の[エディタの書式](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-editor-format.md)が「年月日」の場合は、入力した日付の翌日をUTCに変換した日付を取得します。「日付と時刻（分）」および「日付と時刻（秒）」の場合は、入力した日時をUTCに変換した日時を取得します。  

## 概要

[完了項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)は[エディタの書式](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-editor-format.md)が「年月日」の場合は入力した日付の翌日をデータベースに格納します。データベースに格納する値は次の通りです。

|エディタの書式 | [完了項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)|[開始項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-start-time.md)、[日付項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)|
|---|---|---|
|年月日|画面で入力した日付の翌日|画面で入力した日付|
|日付と時刻（分）|画面で入力した日時|画面で入力した日時|
|日付と時刻（秒）|画面で入力した日時|画面で入力した日時|

サーバスクリプトではデータベースに格納した値を取得後、UTC（協定世界時）に変換した値を返却するため、エディタが「年月日」の場合は、画面入力値の翌日の日付になる場合があります。

## 関連情報

-   [テーブルの管理：項目：完了](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)
-   [テーブルの管理：エディタ：項目の詳細設定：エディタの書式](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-editor-format.md)
-   [テーブルの管理：項目：開始](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-start-time.md)
-   [テーブルの管理：項目：日付](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
