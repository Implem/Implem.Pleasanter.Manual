---
title: フィルタ（選択肢一覧を他の項目の値で絞り込む）
category: エディタ
order: '10000'
status: ''
parts: ''
urlstring: table-management-choice-json-column-filter-expressions
translationKey: table-management-choice-json-column-filter-expressions
shortname: リンク,選択肢一覧のフィルタ,ColumnFilterExpressions
created: 2022-07-25
updated: 2025-02-27
---

## 概要

[選択肢一覧](index.md)にColumnFilterExpressionsを指定することで、選択肢一覧を他の項目の値で絞り込むことができます。

## 制限事項

-   [担当者項目](../../../columns/table-management-owner.md)、[管理者項目](../../../columns/table-management-manager.md)、[分類項目](../../../columns/table-management-class.md)以外では使用できません。
-   [複数選択](../table-management-multiple-selections.md)機能を使用している場合は使用できません。

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

## ColumnFilterExpressionsの指定方法

| 式の種類             | 記述例     | 説明                                                                                                                                                           |
| :------------------- | :--------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 表示名でフィルタ     | [ClassA]   | 指定する項目の選択肢一覧を値と表示名で設定していた場合、項目の[表示名](../table-management-label-text.md)でフィルタします。JSON配列に変換を行ってフィルタします。 |
| 値でフィルタ         | [@ClassA]  | 指定する項目の選択肢一覧を値と表示名で設定していた場合、項目の「値」でフィルタします。JSON配列に変換を行ってフィルタします。                                   |
| 値でそのままフィルタ | =[@ClassA] | JSON配列に変換を行わずに項目の値でフィルタします。フィルタに指定する項目の値を完全一致させたい場合に利用します。                                               |

!!! tip
    [選択肢一覧](index.md)が未設定（自由入力）または[選択肢一覧](index.md)が値のみの場合は、式の種類がいずれの場合でも項目の「値」でフィルタします。

### 設定例①　表示名でフィルタ

画面上の**分類Aの[表示名](../table-management-label-text.md)**で、リンク先のテーブルの分類Xを検索します。画面上の分類Aにポストバックを設定しておくと、分類Aの変更後、即座にリストに反映します。

``` json title="画面上の分類Aの表示名で、リンク先のテーブルの分類Xを検索" linenums="1"
[
    {
        "SiteId": 12345,
        "View": {
            "ColumnFilterExpressions": {
                "ClassX": "[ClassA]"
            }
        }
    }
]
```

画面上の分類Aに「テスト」と記載されている場合、内部的な動作は以下のようになります。

=== "分類Xが「選択肢なし」の場合"

    そのままColumnFilterHashに渡されます。

    ``` json title="分類Xが「選択肢なし」の場合" linenums="1" hl_lines="6"
    [
        {
            "SiteId": 12345,
            "View": {
                "ColumnFilterHash": {
                    "ClassX": "テスト"
                }
            }
        }
    ]
    ```

=== "分類Xが「選択肢あり」の場合"

    左辺が選択肢ありの場合、自動的にJSON配列に変換されて渡されます。

    ``` json title="分類Xが「選択肢あり」の場合" linenums="1" hl_lines="6"
    [
        {
            "SiteId": 12345,
            "View": {
                "ColumnFilterHash": {
                    "ClassX": "[\"テスト\"]"
                }
            }
        }
    ]
    ```

### 設定例②　値でフィルタ

画面上の**分類Aの値**で、リンク先のテーブルの分類Xを検索します。分類Aに値と表示名があり、値を取り出したい場合は`@`を付与します。

``` json title="画面上の分類Aの値で、リンク先のテーブルの分類Xを検索" linenums="1" hl_lines="6"
[
    {
        "SiteId": 12345,
        "View": {
            "ColumnFilterExpressions": {
                "ClassX": "[@ClassA]"
            }
        }
    }
]
```

### 設定例③　値でそのままフィルタ

画面上の分類Aの値をJSON文字列に変換せずに直接渡すことができます。分類Aが複数選択項目の場合、`[@ClassA]`にはJSON形式の文字列が入っています。左辺が選択肢ありの場合、自動的にJSON配列に変換される仕組みがありますが、既にJSONが入っている場合に変換させないよう`=`を記述します。

``` json linenums="1" hl_lines="6"
[
    {
        "SiteId": 12345,
        "View": {
            "ColumnFilterExpressions": {
                "ClassX": "=[@ClassA]"
            }
        }
    }
]
```

右辺に数値項目を使用する場合、`@`をつけないと記号や単位のついた文字列で検索が行われます。

``` json linenums="1" hl_lines="6"
[
    {
        "SiteId": 12345,
        "View": {
            "ColumnFilterExpressions": {
                "ClassX": "=[@NumA]"
            }
        }
    }
]
```

## ColumnFilterExpressionsの動作イメージ

以下のJSONをフィルタ対象とする分類Bの選択肢一覧に設定した場合、サイトID:12345のテーブルの分類Cが設定対象テーブルの分類Aの表示名に一致するレコードでフィルタされます。

分類Aは[自動ポストバック](../table-management-auto-postback.md)をオンにします。

``` json linenums="1"
[
    {
        "SiteId": 12345,
        "View": {
            "ColumnFilterExpressions": {
                "ClassC": "[ClassA]"
            }
        }
    }
]
```

### 例①　表示名でフィルタする場合

下図の例では、上記JSONを「読書感想文集」テーブルの「書籍名（分類B）」の[選択肢一覧](index.md)に記述して、選択肢が絞り込まれるようにしています。編集画面にて「出版社（分類A）」を選択した際の自動ポストバック処理により、「書籍名（分類B）」の選択肢は「出版社（分類A）」の表示名でフィルタされました。「書籍名（分類B）」には、「書籍管理」テーブル（サイトID: 12345）に登録されている「出版社（分類C）」が、選択した「出版社（分類A）」の表示名と一致する書籍のタイトルのみが表示されています。

-   「読書感想文集」テーブルの編集画面

    ![「読書感想文集」テーブルの編集画面。書籍名が出版社で絞り込まれる](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/d06cccc162914a9a8837e341b30250f8.png)

-   「書籍管理」テーブル（サイトID:12345）の一覧画面

    ![「書籍管理」テーブル（サイトID:12345）の一覧画面。フィルタの参照先になる書籍のデータが並ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/9d548d7894a64c499b9ff620dade30c6.png)

### 例②　フィルタ先の分類項目が複数選択の場合

-   「書籍管理」テーブル（サイトID:12345）の一覧画面

    ![「書籍管理」テーブル（サイトID:12345）の一覧画面。分類Cが複数選択](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/2ebf3e83e71b407387785d0a2cf9fbc8.png)

-   「書籍名（分類B）」の式の[選択肢一覧](index.md)を「値でフィルタ」形式で記述した場合

    サイトID:12345の分類Cが設定対象テーブルの分類Aの値にJSON形式の文字列として一致しないため、分類Bには何も選択肢が表示されません。

    ![「値でフィルタ」形式で記述した場合の画面（1/2）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/3c8b23033c6e4f1490871288056ecdef.png)

    ![「値でフィルタ」形式で記述した場合の画面（2/2）。分類Bが空になる](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/d223010fe4274408bd666e101e5179f0.png)

-   「書籍名（分類B）」の[選択肢一覧](index.md)を「値でそのままフィルタ」形式で記述した場合

    サイトID:12345の分類Cが設定対象テーブルの分類Aの値にJSON形式の文字列として一致するため、分類Bにはフィルタされた選択肢が表示されます。

    ![「値でそのままフィルタ」形式で記述した場合。分類Bが絞り込まれる](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/3edb675cb24e425fbe98d01dd532d550.png)

## ユーザの所属グループを選択肢一覧に表示する方法

担当者項目に設定されているユーザの所属しているグループを任意の分類項目の選択肢一覧に表示します。

1.  任意のテーブルを開いてください。
1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  「[テーブルの管理](../../../../../index.md)」をクリックしてください。
1.  「[エディタ](../../../../index.md)」タブをクリックしてください。
1.  「[エディタの設定](../../../index.md)」で「分類A」を有効化してください。
1.  「分類A」を選択し、「詳細設定」を開いてください。
1.  「[選択肢一覧](index.md)」に以下のJSONを記載してください。

    ``` json linenums="1"
    [
        {
            "TableName": "Groups",
            "View": {
                "ColumnFilterExpressions": {
                    "GroupMembers":"[@Owner]"
                }
            }
        }
    ]
    ```

以下のどちらかの条件に一致するグループが選択肢一覧に表示されます。

1. ユーザが所属しているグループ
1. ユーザが所属している組織が所属しているグループ  

そのため、ユーザが直接所属しているグループ、もしくは組織経由でユーザが所属しているグループが絞り込みの対象となります。

**"GroupMembers"がユーザ項目であることが前提条件となります。**

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.3.16.0以降   | 機能追加 |

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](table-management-choices-text-depts.md)
-   [テーブルの管理：項目：担当者](../../../columns/table-management-owner.md)
-   [テーブルの管理：項目：管理者](../../../columns/table-management-manager.md)
-   [テーブルの管理：項目：分類](../../../columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](../table-management-multiple-selections.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../table-management-label-text.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック](../table-management-auto-postback.md)
-   [テーブルの管理](../../../../../index.md)
