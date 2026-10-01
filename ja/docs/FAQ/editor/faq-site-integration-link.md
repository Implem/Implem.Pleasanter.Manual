---
title: サイト統合により複数のテーブルを結合した統合テーブルを親としてリンク設定を行ったとき、子テーブルのリンク項目に選択肢一覧が表示されない
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-site-integration-link
translationKey: faq-site-integration-link
shortname: ''
created: 2019-04-03
updated: 2024-04-29
---

## 回答

選択肢一覧で指定するテーブルIDを統合テーブルではなく、統合元テーブルのIDを記述してください。

---

## 概要

統合テーブルは統合元テーブルのレコードを参照しているだけであり、統合テーブル自体にレコードを持っていないため、選択肢一覧で統合テーブルのIDを指定しても子テーブルの[リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)項目に選択肢は表示されません。

統合テーブルに表示されるレコードを子テーブルのリンク項目に表示させる場合は、統合元テーブルを複数リンク設定する必要があります。
具体的には、子テーブルの[テーブルの管理](../../managers-guide/manage-table/index.md)－[エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)タブにある子テーブルのリンク項目（任意の分類項目）の詳細設定より、[選択肢一覧](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)で下のように記述してください。

```text
[[統合元テーブル1のID]] [[統合元テーブル2のID]] [[統合元テーブル3のID]]
```

## 関連情報

-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードのエディタ画面](../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
