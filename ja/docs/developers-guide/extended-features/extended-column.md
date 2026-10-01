---
title: 拡張項目
category: 拡張機能
order: '0'
status: ''
parts: ''
urlstring: extended-column
translationKey: extended-column
shortname: 拡張項目
ee_notice: columns
created: 2021-04-02
updated: 2025-03-06
---

## 概要

組織の管理、グループの管理、ユーザの管理に[分類項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)などの[項目](../../managers-guide/manage-table/editor/editor-settings/columns/index.md)を追加します。

## 利用上の注意

誤った設定を行うとプリザンターが利用できなくなる可能性がありますので、十分なテストを行った上でご利用ください。

## 拡張項目の設定方法

.\pleasanter\Implem.Pleasanter\App_Data\Parameters\に、CustomDefinitionsフォルダを作成し、配下に以下の構文で拡張したい項目を記載したテキストファイルを作成し、IISを再起動してください。ファイル名は必ずColumn.jsonにしてください。

``` json linenums="1"
{
    "Users_ClassA": {
        "LabelText": "名称",
        "GridEnabled": "1",
        "EditorEnabled": "1",
        "LabelText_en": "Name",
        "LabelText_zh": "名称",
        "LabelText_de": "Name",
        "LabelText_ko": "이름",
        "LabelText_es": "Nombre",
        "LabelText_vn": "Tên"
    },

    "Users_DateA": {
        "LabelText": "DateA",
        "GridEnabled": "1",
        "EditorEnabled": "1"
    },

    "Groups_DescriptionA": {
        "LabelText": "DescriptionA",
        "GridEnabled": "1",
        "EditorEnabled": "1",
        "FieldCss": "field-wide",
        "UpdateAccessControl": "ManageTenant"
    },

    "Depts_CheckA": {
        "LabelText": "CheckA",
        "GridEnabled": "1",
        "EditorEnabled": "1"
    }
}
```

| 項目名              | 説明                                                                                                                                                                                                                                                                                                     |
| :------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| LabelText           | 項目の表示名（日本語）を指定します。                                                                                                                                                                                                                                                                     |
| GridEnabled         | 一覧画面に表示する場合には"1"を入れます。表示しない場合は、この行は不要です。                                                                                                                                                                                                                            |
| EditorEnabled       | 編集画面に表示する場合には"1"を入れます。表示しない場合は、この行は不要です。                                                                                                                                                                                                                            |
| UseSearch           | 検索機能を有効にする場合、trueを指定します。                                                                                                                                                                                                                                                             |
| ChoicesText         | 選択式にする場合には選択肢を入力します。選択肢の区切りには\nを入れます。                                                                                                                                                                                                                                 |
| FieldCss            | [入力項目のスタイル](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-field-css.md)（ノーマル、ワイド、マークダウン）を設定します。"field-normal","field-wide","field-markdown"のいずれかを指定します。スタイルを変更しない場合は、この行は不要です。 |
| CreateAccessControl | 新規作成時にテナント管理者のみがこの項目値を設定できるよう制限する場合"ManageTenant"を指定します。制限しない場合は、この行は不要です。                                                                                                                                                                   |
| UpdateAccessControl | 更新時にテナント管理者のみがこの項目値を変更できるよう制限する場合"ManageTenant"を指定します。制限しない場合は、この行は不要です。                                                                                                                                                                       |
| ReadAccessControl   | テナント管理者のみがこの項目値を閲覧することができるよう制限する場合"ManageTenant"を指定します。制限しない場合は、この行は不要です。                                                                                                                                                                     |
| LabelText_en        | 項目の表示名（英語）を指定します。                                                                                                                                                                                                                                                                       |
| LabelText_zh        | 項目の表示名（中国語）を指定します。                                                                                                                                                                                                                                                                     |
| LabelText_de        | 項目の表示名（ドイツ語）を指定します。                                                                                                                                                                                                                                                                   |
| LabelText_ko        | 項目の表示名（韓国語）を指定します。                                                                                                                                                                                                                                                                     |
| LabelText_es        | 項目の表示名（スペイン語）を指定します。                                                                                                                                                                                                                                                                 |
| LabelText_vn        | 項目の表示名（ベトナム語）を指定します。                                                                                                                                                                                                                                                                 |

## 関連情報

-   [テーブルの管理：項目：分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目](../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力項目のスタイル](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-field-css.md)
