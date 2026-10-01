---
title: 分類項目でユーザ、組織、グループの選択肢を利用したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-class-column-functions
translationKey: faq-class-column-functions
shortname: ''
ee_notice: columns
created: 2019-01-15
updated: 2024-04-29
---

## 回答

[分類項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)の「詳細設定」にて、[選択肢一覧](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)に`[[Users]]`、`[[Depts]]`、`[[Groups]]`を設定してください。

---

## 概要

[分類項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)で[ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)、[組織](../../managers-guide/department-administration/index.md)、[グループ](../../managers-guide/group-administration/index.md)をドロップダウンリストで表示する方法を説明します。

### 選択肢一覧へ記述する式

| 選択肢     | 選択肢一覧へ<br>記述する式 | 説明                                                                                                                                                                                      |
| :--------- | :------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ユーザ     | `[[Users]]`                | テーブルにアクセス権がある[ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)を表示します。   |
| 全ユーザ   | `[[Users*]]`               | テナント全体で登録されている[ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)を表示します。 |
| 全組織     | `[[Depts]]`                | テナント全体で登録されている[組織](../../managers-guide/department-administration/index.md)を表示します。                                                                                  |
| グループ   | `[[Groups]]`               | テーブルにアクセス権として設定されている[グループ](../../managers-guide/group-administration/index.md)を表示します。                                                                                                                |
| 全グループ | `[[Groups*]]`              | テナント全体で登録されている[グループ](../../managers-guide/group-administration/index.md)を表示します。                                                                                                                            |

### 既定値へ記述する式

| 既定値へ<br>記述する式 | 説明                                                                                                                 |
| :--------------------- | :------------------------------------------------------------------------------------------------------------------- |
| `[[Self]]`             | 選択肢一覧に`[[Depts]]`や`[[Users]]`が指定されている際に、ログインしているユーザ情報から既定値を自動的に設定します。 |

## 関連情報

-   [テーブルの管理：項目：分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [組織管理機能](../../managers-guide/department-administration/index.md)
-   [グループ管理機能](../../managers-guide/group-administration/index.md)
