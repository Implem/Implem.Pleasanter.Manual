---
title: ルックアップ機能を使用して組織・ユーザ・グループの情報を取得する
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-lookups-depts
translationKey: faq-lookups-depts
shortname: ''
created: 2021-08-11
updated: 2023-01-05
---

## 概要

ルックアップ機能を使用して、組織・ユーザ・グループの情報を取得する方法を説明します。
ここでは、組織テーブルの情報を取得する設定例をご紹介します。

## 設定例

[選択肢一覧](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)にJSON形式で[リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)を指定します。記述方法は「[テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)」と同様です。
下記の例では、[項目](../../managers-guide/manage-table/editor/editor-settings/columns/index.md)を選択した際に、組織テーブル の分類A（ClassA）を分類C（ClassC）に転記、分類B（ClassB）を分類D（ClassD）に転記、分類C（ClassC）を分類E（ClassE）に転記しています。

##### JSON

```
[
    {
        "TableName": "Depts",
        "Lookups": [
            {
                "From": "ClassA",
                "To": "ClassC",
                "Type": 0
            },
            {
                "From": "ClassB",
                "To": "ClassD",
                "Type": 0
            },
            {
                "From": "ClassC",
                "To": "ClassE",
                "Type": 0
            }                          
        ]
    }
]
```