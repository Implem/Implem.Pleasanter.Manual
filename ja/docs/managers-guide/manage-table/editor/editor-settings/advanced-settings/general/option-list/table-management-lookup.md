---
title: ルックアップ
category: エディタ
order: '10500'
status: ''
parts: ''
urlstring: table-management-lookup
translationKey: table-management-lookup
shortname: リンク,ルックアップ
created: 2021-05-30
updated: 2025-09-16
---

## 概要

[組織](../../../../../../department-administration/index.md)、[グループ](../../../../../../group-administration/index.md)、[ユーザ](table-management-choices-text-users.md)および[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)された[項目](../../../columns/index.md)を選択した際に、選択した[組織](../../../../../../department-administration/index.md)、[グループ](../../../../../../group-administration/index.md)、[ユーザ](table-management-choices-text-users.md)および[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)の[項目](../../../columns/index.md)を転記することができます。例えば商談テーブルから顧客テーブルをリンクしている際に、顧客テーブルの住所項目、電話番号項目などを商談テーブルに転記できます。説明項目等に登録されている画像を転記することも可能です。また、[自動ポストバック](../table-management-auto-postback.md)機能と組み合わせると、マスタ選択後、すぐに値を反映することができます。

## 制限事項

1. ルックアップ機能は[分類項目](../../../columns/table-management-class.md)、[管理者項目](../../../columns/table-management-manager.md)、[担当者項目](../../../columns/table-management-owner.md)に設定できます。
1. [複数選択](../table-management-multiple-selections.md)機能を使用している場合は使用できません。
1. [コメント項目](../../../columns/table-management-comments.md)、[添付ファイル項目](../../../columns/table-management-attachments.md)をFromおよびToに指定することはできません。
1. 「読み取り権限」のない項目をFromに指定した場合、空文字が転記されます。
1. 項目に転記した値が登録されますので、親テーブルで値を変更しても反映されません。
1. [インポート](../../../../../../../users-guide/table/record-authoring/create-records/table-record-import.md)で「IDが一致するレコードを更新する」にした場合、項目が変更になった場合のみ動作します。
1. [組織](../../../../../../department-administration/index.md)、[グループ](../../../../../../group-administration/index.md)、[ユーザ](table-management-choices-text-users.md)および[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)された[項目](../../../columns/index.md)が複数選択の場合には動作しません。
1. Fromに指定した[説明項目](../../../columns/table-management-description.md)に画像が貼り付けられている場合は、その画像も転記されます。ただし、転記された画像は転記元レコードのアクセス権が適用されるため、画像が表示されない可能性があります。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 操作手順

[選択肢一覧](index.md)にJSON形式で「[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)」を指定します。記述方法は「[フィルタ、ソート、表示フォーマット](table-management-choice-json.md)」と同様です。

## 設定例1

下記の例ではサイトID 6 に[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)し、[項目](../../../columns/index.md)を選択した際に、サイトID 6 の分類A（ClassA）を分類B（ClassB）に転記、分類B（ClassB）を分類C（ClassC）に転記、状況（Status）を分類D（ClassD）に転記、および日付A、チェックA、説明Aをそれぞれに転記しています。[状況項目](../../../columns/table-management-status.md)はTypeを 1 に指定し「値」ではなく[表示名](../table-management-label-text.md)を転記します。

``` json title="選択肢一覧" linenums="1"
[
    {
        "SiteId": 6,
        "Lookups": [
            {
                "From": "ClassA",
                "To": "ClassB"
            },
            {
                "From": "ClassB",
                "To": "ClassC"
            },
            {
                "From": "Status",
                "To": "ClassD",
                "Type": 1
            },
            {
                "From": "DateA",
                "To": "DateA"
            },
            {
                "From": "NumA",
                "To": "NumA"
            },
            {
                "From": "CheckA",
                "To": "CheckA"
            },
            {
                "From": "DescriptionA",
                "To": "DescriptionA"
            }
        ]
    }
]
```

## 設定例2

下記の例では[組織](../../../../../../department-administration/index.md)を選択肢に設定し、[組織](../../../../../../department-administration/index.md)を選択した際に、「組織コード」を分類Eに転記します。

``` json title="選択肢一覧" linenums="1"
[
    {
        "TableName": "Depts",
        "Lookups": [
            {
                "From": "DeptCode",
                "To": "ClassE",
                "Type": 0
            }
        ]
    }
]
```

## 設定例3

下記の例では[グループ](../../../../../../group-administration/index.md)を選択肢に設定し、[グループ](../../../../../../group-administration/index.md)を選択した際に、[説明](../table-management-column-description.md)を分類Eに転記します。

``` json title="選択肢一覧" linenums="1"
[
    {
        "TableName": "Groups",
        "Lookups": [
            {
                "From": "Body",
                "To": "ClassE",
                "Type": 0
            }
        ]
    }
]
```

## 設定例4

下記の例では[ユーザ](table-management-choices-text-users.md)を選択肢に設定し、[ユーザ](table-management-choices-text-users.md)を選択した際に、組織名を分類E、説明を説明A、メールアドレスを分類Mに転記します。

``` json title="選択肢一覧" linenums="1"
[
    {
        "TableName": "Users",
        "Lookups": [
            {
                "From": "Dept",
                "To": "ClassE",
                "Type": 1
            },
            {
                "From": "Body",
                "To": "DescriptionA"
            },
            {
                "From": "MailAddresses",
                "To": "ClassM"
            }
        ]
    }
]

```

## 設定例5

下記の例では[グループ](../../../../../../group-administration/index.md)を選択肢に設定し、[グループ](../../../../../../group-administration/index.md)を選択した際に、「グループ名称」を分類Eに転記します。このとき分類Eに値が設定されている場合は上書きせず、分類Eに値が設定されていない場合のみ転記します。

``` json title="選択肢一覧" linenums="1"
[
    {
        "TableName": "Groups",
        "Lookups": [
            {
                "From": "GroupName",
                "To": "ClassE",
                "Type": 0,
                "Overwrite": false
            }
        ]
    }
]
```

## 設定例6

下記の例では[グループ](../../../../../../group-administration/index.md)を選択肢に設定し、[グループ](../../../../../../group-administration/index.md)を選択した際に、「グループ名称」を分類Aに転記します。このとき分類Aに値が設定されている場合でも「グループ名称」で上書きして転記します。

``` json title="選択肢一覧" linenums="1"
[
    {
        "TableName": "Groups",
        "Lookups": [
            {
                "From": "GroupName",
                "To": "ClassA",
                "Type": 0,
                "OverwriteForm": true
            }
        ]
    }
]
```

## 設定内容

|No|選択肢|説明|
|:----|:----|:----|
|1|From|転記元の[テーブル](../../../../../../../users-guide/table/index.md)の[データベースのカラム名](../../../../../../../developers-guide/dev-column-name.md)を指定します。|
|2|To|転記先の[テーブル](../../../../../../../users-guide/table/index.md)の[データベースのカラム名](../../../../../../../developers-guide/dev-column-name.md)を指定します。|
|3|Type|値を転記する場合には 0 を指定します。表示名を転記する場合には 1 を指定します。Typeは省略可能です。省略した場合の既定値は 0 です。|
|4|Overwrite|Toで指定した項目に既に値が設定されている場合は上書きせず、値が設定されていない場合のみ転記したい場合は false を指定します。Overwriteは省略可能です。省略した場合の既定値は true です。|
|5|OverwriteForm|Toで指定した項目に値を必ず転記したい場合はtrueを指定します。OverwriteFormは省略可能です。省略した場合の既定値は false です。なお、ユーザによる手動入力した場合であっても上書き転記します。|

## 詳細情報

1. [状況項目](../../../columns/table-management-status.md)や[分類項目](../../../columns/table-management-class.md)で「値」と[表示名](../table-management-label-text.md)が分かれている項目をFromに指定する場合には、Typeの設定が重要です。Toも同様に「値」と[表示名](../table-management-label-text.md)が分かれている場合には 0 を指定しますが、表示名を文字列として転記したい場合には 1 を指定します。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.27.0 以降|機能追加|
|1.2.2.0以降|[組織](../../../../../../department-administration/index.md)、[グループ](../../../../../../group-administration/index.md)、[ユーザ](table-management-choices-text-users.md)のルックアップ機能を追加|
|1.3.10.0以降|上書きを制御するスイッチ機能（Overwrite）を追加|
|1.4.13.0 以降|利用できる項目に[管理者項目](../../../columns/table-management-manager.md)、[担当者項目](../../../columns/table-management-owner.md)を追加|

## 関連情報

-   [組織管理機能](../../../../../../department-administration/index.md)
-   [グループ管理機能](../../../../../../group-administration/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](table-management-choices-text-users.md)
-   [応用編：リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：項目](../../../columns/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック](../table-management-auto-postback.md)
-   [テーブルの管理：項目：分類](../../../columns/table-management-class.md)
-   [テーブルの管理：項目：管理者](../../../columns/table-management-manager.md)
-   [テーブルの管理：項目：担当者](../../../columns/table-management-owner.md)
-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](../table-management-multiple-selections.md)
-   [テーブルの管理：項目：コメント](../../../columns/table-management-comments.md)
-   [テーブルの管理：項目：添付ファイル](../../../columns/table-management-attachments.md)
-   [組織管理機能：インポート](../../../../../../department-administration/dept-import.md)
-   [テーブルの管理：項目：説明](../../../columns/table-management-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](table-management-choices-text-depts.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](table-management-choice-json.md)
-   [テーブルの管理：項目：状況](../../../columns/table-management-status.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../table-management-label-text.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../table-management-column-description.md)
-   [テーブル機能](../../../../../../../users-guide/table/index.md)
-   [項目名とデータベース上のカラム名の対応](../../../../../../../developers-guide/dev-column-name.md)