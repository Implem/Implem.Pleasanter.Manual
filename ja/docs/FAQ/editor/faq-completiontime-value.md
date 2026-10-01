---
title: サーバスクリプトやAPIで完了の値を取得すると画面表示の翌日になっている
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-completiontime-value
translationKey: faq-completiontime-value
shortname: ''
created: 2025-05-08
updated: 2025-05-08
---

## 回答

仕様です。「完了」項目の[エディタの書式](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-editor-format.md)が「年月日」の場合、画面入力した日付の翌日がデータベース上登録される仕様です。

---

## 概要

「完了」項目は[エディタの書式](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-editor-format.md)が「年月日」の場合に限り、画面から入力した日付の翌日（の0時0分0秒）が登録される仕様です。そのため、サーバスクリプトやAPIではデータベース上の値をそのまま返却しますので、画面上の日付の翌日を取得します。独自のスクリプトで「完了」項目の値を操作する場合はご注意ください。なお、[エディタの書式](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-editor-format.md)を「年月日」以外に設定した場合は画面から入力した日時がそのまま登録されます。

|画面入力値|API|サーバスクリプト|スクリプト（$p.apiGet）|スクリプト（$p.getValue）|

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：エディタの書式](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-editor-format.md)