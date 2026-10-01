---
title: リンク
category: 操作ガイド（応用編）
order: '30'
status: ''
parts: ''
urlstring: advanced-operations-link
translationKey: advanced-operations-link
shortname: 応用編,リンク,サマリ,ドロップダウンリスト,フィルタ,ルックアップ
created: 2023-06-29
updated: 2024-07-08
---

## 概要

テーブル間で親子関係を設定できます。リンクを設定することでより使いやすい画面を作ることができます。

1.  親テーブルのタイトルを子テーブルの分類項目にドロップダウンリストとして表示。  
1.  編集画面にリンクレコードの一覧および子テーブルへのレコード新規作成ボタンを表示。
1.  子レコードの総件数や子レコードの数値項目の合計や平均などの「[サマリ](../../../managers-guide/manage-table/summaries/index.md)」を自動計算。

## 1. ドロップダウンリスト

ドロップダウンリストは[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)をJSON形式で記述することでカスタマイズができます。

### 1-1．表示内容

デフォルトでは親テーブルの[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)がドロップダウンリストとして表示します。

![親テーブルのタイトルが並ぶドロップダウンリスト](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/6b31704e87e24bc6913463d83f8816ad.png)

[検索機能を使う](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)を有効化した場合、[表示フォーマット](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)を指定することで、親テーブルのタイトル以外の項目をリストに表示できます。

#### 例1. ユーザの氏名に加えてメールアドレスをリストに表示

``` json title="JSON" linenums="1" hl_lines="4"
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

![氏名とメールアドレスを並べて表示したドロップダウンリスト](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/db9cd06e19d8476b9b68c6d7a19b1e24.png)

#### 例2. 親テーブル（サイトID：12345）の分類A、分類B、分類Cをリスト表示

``` json title="JSON" linenums="1" hl_lines="5"
[
    {
        "SiteId": 12345,
        "NoAddButton": false,
        "SearchFormat": "[ClassA] - [ClassB] - [ClassC]"
    }
]
```

![分類A・分類B・分類Cを並べて表示したドロップダウンリスト](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/16e2f7f675684cdd922cc59dfaace4c2.png)

[検索機能を使う](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)が無効になっている場合は表示フォーマットの指定は適用されません。

### 1-2．フィルタ

デフォルトでは親テーブルの参照可能なレコードをリスト表示しますが、リストの内容を任意に絞り込むことができます。  
絞り込みは主に3つの方法となります。

1.  「項目連携機能」で絞り込み
1.  固定値で絞り込み
1.  画面の項目で動的絞り込み

#### 項目連携で絞り込み

画面上に設定した親子関係にある2つのドロップダウンリスト（A、B）を連携させ、ドロップダウンAで選択した内容でドロップダウンリストBのリスト内容を絞り込みします。都道府県マスタと市区町村マスタのように都道府県を選択することで、市区町村のリスト内容を絞り込むようなケースで利用できます。

![ドロップダウンAの選択でドロップダウンBの内容が絞り込まれる例](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/7fdb83f63eb24b5993603029ed7fd699.png)

#### 固定値で絞り込み

あらかじめ定数を指定して絞り込みします。状況が"未完了"の未完了タスクリスト、金額が100万円以上の高額商品リストなどのように元となるリストから固定値でリスト内容を絞り込むようなケースで利用できます。

#### 例. 100万円以上の仕入レコードのみドロップダウンリスト表示

``` json title="JSON" linenums="1" hl_lines="5"
[
    {
        "SiteId": 127,
        "NoAddButton": false,
        "View": {
            "ColumnFilterHash": {
                "NumA": "[\"1000000,\"]"
            }
        }
    }
]
```

![固定値で絞り込んだドロップダウンリストの表示結果](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/15aa98167de04751af7f817611bce8c1.png)

#### 画面の項目で動的絞り込み

あらかじめ画面の項目を指定しておき、入力された値に応じてリスト内容を動的に絞り込みます。項目連動と異なり、親子関係にある画面の任意の項目（分類、数値、日付等）をもとにリスト内容を絞り込みます

#### 例. 分類Aで選択した内容で分類Cのドロップダウンリストの内容を絞り込む

``` json title="JSON" linenums="1" hl_lines="6"
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

![分類Aの選択に応じて絞り込まれた分類Cのドロップダウンリスト](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/af93766bd6ee48aca1b483bc4b3bb2be.png)

### 1-3．ルックアップ

ドロップダウンリストで選択した情報の別の項目を転記することができます。  
例えば、商談テーブルから顧客テーブルをリンクしている構成において、顧客を選択したときに顧客テーブルの住所、電話項目などを商談テーブルに転記できます。

#### 例2. 選択した顧客の住所、連絡先を自動転記

``` json title="JSON" linenums="1" hl_lines="4-13"
[
    {
        "SiteId": 125,
        "Lookups": [
            {
                "From": "ClassA",
                "To": "ClassC"
            },
            {
                "From": "ClassB",
                "To": "ClassD"
            }
        ]
    }
]
```

##### マスタ内容

![ルックアップ元となるマスタのレコード内容](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/e1c64ea5c3984620af4625e7318a5d7f.png)

##### 動作結果

![ルックアップで住所と連絡先が転記された編集画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/ce470d70ce2a4c98a6e2f0654cdbf935.png)

[自動ポストバック](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-auto-postback.md)機能が無効になっている場合、マスタ選択後、すぐに値が反映されません。

## 2. リンクの一覧、作成ボタン

リンクを設定すると、編集画面の最下段にリンクの情報「リンクしたアイテムの作成」、「リンク」が表示します。

### リンクしたアイテムの作成：レコード作成ボタン

親レコードの編集画面において、子テーブルに対して新規作成するためのボタンが表示されます。ボタン名は子テーブル名です。子テーブル側から親レコードを新規作成することはできません。設定により、ボタンを非表示にすることができます。

### リンク：リンクレコード一覧

編集画面で表示したレコードに関連するリンクレコードの一覧が表示されます。リンク先（親テーブル）のレコード一覧およびリンク元（子テーブル）のレコード一覧が表示します。設定により、非表示にすることができます。

![編集画面の最下段に表示されるリンクの一覧と作成ボタン](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/d63581cdc3a34b52a807ee37fe69428c.png)

### 並び順

リンクの情報の並び順は下記の2つの方法で変更できます。

1.  [テーブルの管理](../../../managers-guide/manage-table/index.md)、[エディタ](../../table/record-authoring/edit-records/table-editor.md)でリンク項目を有効化し、任意の順序で並べる

    [エディタ](../../table/record-authoring/edit-records/table-editor.md)で設定することで順序だけでなく、画面の上部や別タブなど任意の場所に表示することができます。その際、ボタンとレコード一覧がセットで表示します。

    ![エディタでリンク項目を有効化し、表示位置を並べ替える画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/0f9125fd892f4491bc4547c11eac7a33.png)

1.  子テーブル側でリンクした項目の選択肢一覧で「priority」キーワードを指定し、並び順を指定する

    デフォルトの表示形式でボタンおよびレコード一覧の並び順を自由に並び変えることができます。

#### 子テーブル側の選択肢の設定

![子テーブルの選択肢一覧に priority を指定した設定](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/4d6a559639d8432996d4c2e42ca9a921.png)

#### 表示結果

![priorityの指定に従って並んだリンクのボタンと一覧](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/1d8001ffd4764ef0b758569af0300728.png)

## 3. 選択肢一覧で設定可能なJSONパラメータ

| リンク対象             | 項目名                        | 説明                                                                                                                                                                                     |
| :--------------------- | :---------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 組織、グループ、ユーザ | TableName                     | Depts、Groups、Usersを指定することで組織、グループ、ユーザを選択肢に表示します。                                                                                                         |
| 組織、グループ、ユーザ | MembersOnly                   | Depts、Groups、Users指定時に使用。アクセス権を付与されている組織、グループ、ユーザのみ表示します。                                                                                       |
| 組織、グループ、ユーザ | ExcludeMe                     | Depts、Groups、Users指定時に使用。自分および自分の組織を含めない場合、trueを指定します。この項目は省略可能です。                                                                         |
| テーブル               | SiteId                        | リンク先のテーブルのサイトIDを指定します。                                                                                                                                               |
| テーブル               | Priority                      | リンクテーブルの表示順序を制御                                                                                                                                                           |
| テーブル               | NoAddButton                   | リンクしたアイテムの作成ボタンを非表示にする場合、trueを指定します。この項目は省略可能です。                                                                                             |
| 共通                   | SearchFormat                  | [検索機能を使う](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)を有効化した際の表示フォーマットを指定します。     |
| 共通                   | View: ColumnFilterHash        | [JSONデータレイアウト：View](../../../developers-guide/json-data-layout/api-view/index.md)を使用して選択肢を特定の項目でフィルタして表示します。フィルタする値は定数で指定することができます。 |
| 共通                   | View: ColumnFilterExpressions | [JSONデータレイアウト：View](../../../developers-guide/json-data-layout/api-view/index.md)を使用して選択肢を特定の項目でフィルタして表示します。フィルタする値は変数で指定することができます。 |
| 共通                   | View: ColumnSorterHash        | [JSONデータレイアウト：View](../../../developers-guide/json-data-layout/api-view/index.md)を使用して選択肢を特定の項目でソートして表示します。                                                 |
| 共通                   | Lookups                       | 「[ルックアップ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-lookup.md)」機能を使用して項目を転記します。この項目は省略可能です。 |

## 4. サマリ

リンク設定した「子テーブル」のレコード件数や[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)の合計、平均、最大、最小を親テーブルの指定した[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)に格納します。子レコードの追加・更新・削除と合わせて動作します。

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../managers-guide/tenant-administration/tenant-logo.md)
-   [テーブルの管理：エディタ：項目の詳細設定：検索機能を使う](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-auto-postback.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードのエディタ画面](../../table/record-authoring/edit-records/table-editor.md)
-   [開発者ガイド：JSONデータレイアウト：View](../../../developers-guide/json-data-layout/api-view/index.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
