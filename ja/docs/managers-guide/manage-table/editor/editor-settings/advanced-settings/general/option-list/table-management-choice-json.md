---
title: フィルタ、ソート、表示フォーマット
category: エディタ
order: '10000'
status: ''
parts: ''
urlstring: table-management-choice-json
translationKey: table-management-choice-json
shortname: リンク,選択肢一覧のフィルタ、ソート、表示フォーマット,フィルタ,ソート,表示フォーマット
created: 2021-04-05
updated: 2024-11-12
---

## 概要

[選択肢一覧](index.md)をJSON形式で記述することで、カスタマイズされた選択肢一覧を使用できます。

## 制限事項

-   [担当者項目](../../../columns/table-management-owner.md)、[管理者項目](../../../columns/table-management-manager.md)、[分類項目](../../../columns/table-management-class.md)以外では使用できません。

## 必要な権限

![サイトの管理権限](../../../../../../../assets/badge_manage_site.svg)

## 操作手順

1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  「[テーブルの管理](../../../../../index.md)」をクリックしてください。
1.  「[エディタ](../../../../index.md)」タブをクリックしてください。
1.  「[エディタの設定](../../../index.md)」で次のいずれかの項目を選択し、「詳細設定」を開いてください。
    -   [担当者項目](../../../columns/table-management-owner.md)
    -   [管理者項目](../../../columns/table-management-manager.md)
    -   [分類項目](../../../columns/table-management-class.md)
1.  「[選択肢一覧](index.md)」にJSON形式で選択肢の表示方法を記述してください。

### 組織、グループ、ユーザの場合

| 項目名                        | 説明                                                                                                                                          |
| :---------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| TableName                     | Depts、Groups、Usersを指定することで組織、グループ、ユーザを選択肢に表示します。                                                              |
| MembersOnly                   | Depts、Groups、Users指定時に使用。アクセス権を付与されている組織、グループ、ユーザのみ表示します。                                            |
| SearchFormat                  | [検索機能を使う](../table-management-use-search.md)を有効化した際の表示フォーマットを指定します。                                                |
| View: ColumnFilterHash        | [JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)を使用して選択肢を特定の項目でフィルタして表示します。フィルタする値は定数で指定することができます。 |
| View: ColumnFilterExpressions | [JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)を使用して選択肢を特定の項目でフィルタして表示します。フィルタする値は変数で指定することができます。 |
| View: ColumnSorterHash        | [JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)を使用して選択肢を特定の項目でソートして表示します。                                                 |

![分類項目の詳細設定の「選択肢一覧」にJSONを記述する欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/a57c569cb6eb455dbaea2d4b272e9f20.png)

#### 設定例

``` json title="ユーザテーブルから「名前 - 組織」の形式、組織、名前の昇順でリストを表示" linenums="1"
[
    {
        "TableName": "Users",
        "MembersOnly": true,
        "SearchFormat": "[Name] - [Dept]",
        "View": {
            "ColumnSorterHash": {
                "DeptCode": "asc",
                "Name": "asc"
            }
        }
    }
]
```

``` json title="ユーザテーブルから「名前 - メールアドレス」の形式、名前の昇順でリストを表示" linenums="1"
[
    {
        "TableName": "Users",
        "SearchFormat": "[Name] - [MailAddresses]",
        "View": {
            "ColumnSorterHash": {
                "Name": "asc"
            }
        }
    }
]
```

``` json title="ユーザテーブルから指定した組織コードに属するユーザを抽出して表示" linenums="1"
[
    {
        "TableName": "Users",
        "MembersOnly": false,
        "SearchFormat": "[Name] - [Dept]",
        "View": {
            "ColumnFilterHash": {
                "DeptCode":"[\"200600\",\"200610\",\"200620\"]"
            },
            "ColumnFilterSearchTypes":{
                "DeptCode": "ExactMatchMultiple"
            }
        }
    }
]
```

??? tip "検索ダイアログでの表示例"

    `SearchFormat`で指定したフォーマット`"[Name] - [Dept]"`で表示されます。

    ![「[Name] - [Dept]」の形式で選択肢が表示された検索ダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/226b05f2ba4a425da02146a81432d97f.png)

``` json title="ユーザテーブルから指定したグループIDに属するユーザを抽出して表示" linenums="1"
[
    {
        "TableName": "Users",
        "View": {
            "ColumnFilterHash": {
                "Groups": "[1,2]"
            }
        }
    }
]
```

### テーブルへのリンクの場合

| 項目名                        | 説明                                                                                                                                                                  |
| :---------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SiteId                        | リンク先のテーブルのサイトIDを指定します。                                                                                                                            |
| Priority                      | [リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)機能を使用して、リンクテーブルの表示順序を制御できます。                                                                         |
| NoAddButton                   | リンクしたアイテムの作成ボタンを非表示にする場合、trueを指定します。この項目は省略可能です。                                                                          |
| NotReturnParentRecord         | リンクしたアイテムの作成ボタンで子レコードを作成後、作成したレコードの編集画面に留まるようにしたい場合に、trueを指定します。この項目は省略可能です。                  |
| SearchFormat                  | [検索機能を使う](../table-management-use-search.md)を有効化した際の表示フォーマットを指定します。この項目は省略可能です。                                                |
| View: ColumnFilterHash        | [JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)を使用して選択肢を特定の項目でフィルタして表示します。フィルタする値は定数で指定することができます。この項目は省略可能です。 |
| View: ColumnFilterExpressions | [JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)を使用して選択肢を特定の項目でフィルタして表示します。フィルタする値は変数で指定することができます。この項目は省略可能です。 |
| View: ColumnSorterHash        | [JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)を使用して選択肢を特定の項目でソートして表示します。この項目は省略可能です。                                                 |
| Lookups                       | [ルックアップ](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)機能を使用して項目を転記します。この項目は省略可能です。                                                                   |

#### 設定例

下記の例では、サイトID:12345のテーブルでチェックAがオンになっているレコードで、タイトルの昇順でリストを表示します。値を選択すると、リンク先の分類Aを分類Bに転記し、リンク先の分類Bを分類Cに転記します。

``` json title="選択肢一覧" linenums="1"
[
    {
        "SiteId": 12345,
        "NoAddButton": false,
        "View": {
            "ColumnFilterHash": {
                "CheckA": true
            },
            "ColumnSorterHash": {
                "Title": "asc"
            }
        },
        "Lookups": [
            {
                "From": "ClassA",
                "To": "ClassB",
                "Type": 0
            },
            {
                "From": "ClassB",
                "To": "ClassC",
                "Type": 0
            }
        ]
    }
]
```

### 選択肢に自分および自分の組織を含めない場合

選択肢一覧のJSONにExcludeMeを指定することで選択肢に自分および自分の組織を含めないことが可能です。

!!! tip

    プロセスボタンを用いた承認のワークフローなどで、ログインユーザ自身を承認者として選択させたくない場合などに利用してください。

``` json title="選択肢一覧" linenums="1"
[
    {
        "TableName": "Users",
        "ExcludeMe": true
    }
]
```

!!! danger "注意事項"

    -   「[エディタの設定](../../../index.md)」の既定値に`[[Self]]`を指定した場合は、自分および自分の組織が設定されます。原則として`"ExcludeMe": true`を指定しないようにしてください。

        [FAQ：分類項目でユーザ、組織、グループの選択肢を利用したい](../../../../../../../FAQ/editor/faq-class-column-functions.md)

    -   ログインユーザ／所属組織設定ボタンは「[スタイル](../../../../../styles/index.md)」の設定`display: none;`などにより非表示としてください。

        [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ログインユーザ設定ボタン](table-management-choices-text-own-user.md)

### ColumnFilterExpressionsの指定方法

選択肢一覧を他の項目の値で絞り込む`ColumnFilterExpressions`の指定方法は、以下のマニュアルを参照してください。

[テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ（選択肢一覧を他の項目の値で絞り込む）](table-management-choice-json-column-filter-expressions.md)

## 対応バージョン

| 対応バージョン | 内容                                                            |
| :------------- | :-------------------------------------------------------------- |
| 1.4.10.0以降   | テーブルへのリンクの場合の設定項目にNotReturnParentRecordを追加 |

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](table-management-choices-text-depts.md)
-   [テーブルの管理：項目：担当者](../../../columns/table-management-owner.md)
-   [テーブルの管理：項目：管理者](../../../columns/table-management-manager.md)
-   [テーブルの管理：項目：分類](../../../columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：検索機能を使う](../table-management-use-search.md)
-   [開発者ガイド：JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)
-   [応用編：リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [FAQ：分類項目でユーザ、組織、グループの選択肢を利用したい](../../../../../../../FAQ/editor/faq-class-column-functions.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ログインユーザ設定ボタン](table-management-choices-text-own-user.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ（選択肢一覧を他の項目の値で絞り込む）](table-management-choice-json-column-filter-expressions.md)
