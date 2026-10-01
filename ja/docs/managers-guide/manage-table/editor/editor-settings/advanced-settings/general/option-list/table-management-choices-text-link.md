---
title: リンク
category: エディタ
order: '8000'
status: ''
parts: ''
urlstring: table-management-choices-text-link
translationKey: table-management-choices-text-link
shortname: リンク
created: 2019-04-30
updated: 2024-11-12
---

## 概要

テーブル間に親子関係を設定することができます。親テーブルで管理しているレコードのタイトルを、子テーブルの分類項目にプルダウンメニューとして表示することができます。期限付きテーブルや記録テーブルのテーブル間で親子関係が設定されると、親となるテーブルのエディタ画面に、子レコードを作成するボタンが表示されます。このボタンから子レコードを作成すると親子双方のエディタ画面に相互リンクが作成されます。相互リンクの一覧に表示する項目はテーブルの管理によりカスタマイズできます。Wikiを親テーブルに設定した場合は、wikiに記載した内容を分類項目で表示することができます。子テーブルのテーブルの管理で分類項目に親テーブルのサイトIDを指定することで設定します。また、自テーブルのサイトIDを指定した場合、テーブル内で階層構造を作ることができます。

## 制限事項

-   [分類項目](../../../columns/table-management-class.md)以外では使用できません。

## 前提条件

-   設定を行うには「サイトの管理権限」が必要です。

## 操作手順

テーブルに親子関係を設定するための手順です。例として、「WBS」テーブルと「課題管理」テーブルを用意しました。「WBS」テーブルを親、「課題管理」テーブルを子としてリンクを設定します。リンク設定する方法は、テーブルの「ドラッグ・アンド・ドロップ」と個々の[テーブルの管理](../../../../../index.md)の2種類あります。

![リンクの例に使う「WBS」テーブルと「課題管理」テーブル](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/4a25ff52b1f7465582a133dff16b5a8c.png)

## ドラッグ・アンド・ドロップで設定する方法

テーブル同士をドラッグ・アンド・ドロップでリンクすることが可能です。この操作はサイトの管理権限が必要です。

1.  サイトメニューで子テーブルになる「課題管理」テーブルをドラッグし、親サイトになる「WBS」テーブルにドロップしてください。
1.  リンクの設定についてポップアップが表示されます。リンクを設定する子テーブルの分類項目および表示名を設定してください。その後、「作成ボタン」をクリックしてください。
1.  リンクの作成可否を確認するポップアップが表示されますので、「OK」ボタンをクリックしてください。
1.  「リンクの作成が完了しました。」とメッセージが表示されたら完了です。

    ![ドラッグ・アンド・ドロップでリンクを作成する操作の画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/bf95e88a3cfe49bdb923547c11f947c3.png)

## テーブルの管理で設定する方法

テーブル同士をサイトIDでリンクすることが可能です。この操作はサイトの管理権限が必要です。

1.  「WBS」テーブルの一覧画面を開き、URLに表示されているサイトIDを控えます。
1.  「課題管理」テーブルを開き、管理/テーブルの管理をクリックします。
1.  [エディタ](../../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを選択し、[選択肢一覧](index.md)から任意の分類項目を有効化します。
1.  「現在の設定」に表示された分類項目を選択し、詳細設定ボタンをクリックします。
1.  [選択肢一覧](index.md)に先程控えたサイトIDを記入し、角括弧で2重に囲います。その後、更新ボタンをクリックします。

    ``` text title="角括弧で2重に囲う際の記述例"
    [[100]]
    ```

1.  コマンドボタンエリアにある「更新」ボタンをクリックします。

    ![テーブルの管理でサイトIDを記入してリンクを設定する画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/103cf12ca840433ba306a146c9c8d289.png)

## リンクされたレコードの一覧表項目の設定方法

リンクされたレコードの一覧表の項目を変更することができます。この操作はサイトの管理権限が必要です。

1.  対象のテーブルを開きます。
1.  「管理」メニューから[テーブルの管理](../../../../../index.md)をクリックします。
1.  [リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)タブを開きます。
1.  下表に従い設定を行います。

    |項目名|説明|設定方法|
    |:---|:---|:---|
    |現在の設定|リンク画面に表示する項目|任意の項目の並び替え、無効化|
    |選択肢一覧|リンク画面に表示可能な項目|任意の項目を有効化|

1.  コマンドボタンエリアにある「更新」ボタンをクリックします。

## リンクしたアイテムの作成ボタンを非表示にする設定方法

テーブル間でリンクが設定されている状態において、親テーブル側で表示される「リンクしたアイテムの作成ボタン」を非表示にすることができます。この操作はサイトの管理権限が必要です。

1.  リンクが設定された子テーブルを開きます。
1.  ナビゲーションメニューより「管理」－[テーブルの管理](../../../../../index.md)をクリックします。
1.  [エディタ](../../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを選択し、現在リンクが設定されている分類項目を選択し、詳細設定ボタンをクリックします。
1.  [選択肢一覧](index.md)でサイトIDの後ろにNoAddButtonを加えます。

    ``` text title="NoAddButtonの記述例"
    [[100,NoAddButton]]
    ```

1.  コマンドボタンエリアにある「更新」ボタンをクリックします。

## リンクしたアイテムを作成後に親テーブル側に戻らないようにする設定

親テーブルの「リンクしたアイテムの作成ボタン」をクリックして子テーブルのレコードを作成すると、通常は親レコードの編集画面に戻ります。この設定を行うことで、作成したレコードの編集画面に留まることができます。

1.  リンクが設定された子テーブルを開きます。
1.  ナビゲーションメニューより「管理」－[テーブルの管理](../../../../../index.md)をクリックします。
1.  [エディタ](../../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを選択し、現在リンクが設定されている分類項目を選択し、詳細設定ボタンをクリックします。
1.  [選択肢一覧](index.md)でサイトIDの後ろにNotReturnParentRecordを加えます。

    ``` text title="NotReturnParentRecordの記述例"
    [[100,NotReturnParentRecord]]
    ```

1.  コマンドボタンエリアにある「更新」ボタンをクリックします。

## リンクの一覧に対して既定のビューの設定方法

[ビュー機能](../../../../../../../users-guide/table/record-authoring/data-analysis/table-record-view.md)と組み合わせることで、エディタ画面に表示されるリンクの一覧に対して、ビューで指定した一覧項目やフィルタ、ソートを適用することができます。事前準備として、子テーブル側で[ビューの設定](../../../../../../../users-guide/table/record-authoring/data-analysis/table-record-view.md)を行ってください。[一覧](../../../../../grid/index.md)タブや[フィルタ](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)タブ、[ソート](table-management-choice-json.md)タブで設定した内容が利用できます。この操作はサイトの管理権限が必要です。

1.  リンクが設定された子テーブルを開きます。
1.  ナビゲーションメニューより「管理」－[テーブルの管理](../../../../../index.md)をクリックします。
1.  [リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)タブを選択し、[既定のビュー](../../../../../grid/table-management-default-view.md)にリンクの一覧に対して適用するビューを選択します。
1.  コマンドボタンエリアにある「更新」ボタンをクリックします。

## リンクした分類項目の取得件数の上限設定方法

パフォーマンスの悪化を防止するため、リンク先のレコード件数が一定数以上の場合、その上限を設定しています。
上限値を変更する場合は、[General.json](../../../../../../../setup/parameters/general.json.md)のDropDownSearchPageSizeに指定してください。既定値は500件です。
また、上限値を超えたレコードが存在する場合は、検索機能を有効化してください。

検索機能の有効化は下記のとおり設定してください。

1.  「[テーブルの管理](../../../../../index.md)」を開きます。
2.  「エディタタブ」を開きます。
3.  対象の項目の「詳細設定」を開きます。
4.  [検索機能を使う](../table-management-use-search.md)にチェックを入れ、「変更」ボタンをクリックします。

    ![項目の詳細設定で「検索機能を使う」にチェックを入れる画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/8b1f7e6396984385b2a4e0a60abbc098.png)

## リンクの解除方法

一度設定したリンクは、下記の手順で解除できます。

1.  子テーブルを開きます。
1.  ナビゲーションメニューより「管理」－「[テーブルの管理](../../../../../index.md)」をクリックします。
1.  管理画面にて「[エディタ](../../../../index.md)」タブを選択します。
1.  リンクが設定されている項目の詳細設定を開き、選択肢に記載されている`[[999]]`の文字を削除することでリンクを解除できます。999は親のサイトIDです。
1.  コマンドボタンエリアにある「更新」ボタンをクリックします。

## リンクテーブルエリアにあるリンク情報の表示順序の制御方法

親レコードの編集画面に表示されるリンク情報の表示順序を以下の手順で制御することが可能です。「リンクしたアイテムの作成」にある子テーブルのレコードを作成するボタンの表示順序も制御されます。

1.  リンクが設定された子テーブルを開きます。
1.  ナビゲーションメニューより「管理」－[テーブルの管理](../../../../../index.md)をクリックします。
1.  [エディタ](../../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを選択し、現在リンクが設定されている分類項目を選択し、詳細設定ボタンをクリックします。
1.  選択肢一覧に下記JSONの内容を入力し、変更ボタンをクリックします。

    ``` json title="SiteIdには親サイトのサイトIDを、Priorityには優先度（数値）を指定"
    [
        {
            "SiteId": 123,
            "Priority": 100
        }
    ]
    ```

1.  コマンドボタンエリアにある「更新」ボタンをクリックします。

### 設定例

下記の例では以下のようなテーブル構成があることを前提としております。

-   親テーブル  
    サイト名：顧客マスタ  
    サイトID：123
-   子テーブル①  
    サイト名：商談  
    サイトID：456
-   子テーブル②  
    サイト名：担当者マスタ  
    サイトID：789

#### デフォルト（`"Priority"`の設定なし）の場合

!["Priority" を設定していない場合のリンクの表示順](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/accd64e7a3124e3da7c13d01add0c29c.png)

#### 担当者マスタの分類項目の選択肢一覧に`"Priority"`を設定している場合

担当者マスタの分類項目の選択肢一覧に上記JSONの内容を設定した場合は以下のように表示されます。`"Priority"`の設定がある方のリンク情報が先に表示されます。

![担当者マスタにのみ "Priority" を設定した場合のリンクの表示順](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/e462023a226e43eab955aa1fab63c08a.png)

#### 商談、担当者マスタの各分類項目の選択肢一覧に`"Priority"`を指定している場合

商談の分類項目の`"Priority"`に100、担当者マスタの分類項目の`"Priority"`に200を設定した場合は以下のように表示されます。`"Priority"`に設定した値が小さい方のリンク情報が先に表示されます。

![商談と担当者マスタの両方に "Priority" を設定した場合のリンクの表示順](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/e82f7ed157e548f49085119b864cd817.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.10.0 以降|リンクしたアイテムを作成後に親テーブル側に戻らないようにする設定（NotReturnParentRecord）を追加|

## 関連情報

-   [テーブルの管理：項目：分類](../../../columns/table-management-class.md)
-   [テーブルの管理](../../../../../index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](table-management-choices-text-depts.md)
-   [応用編：リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブル機能：レコードのビューの切り替え](../../../../../../../users-guide/table/record-authoring/data-analysis/table-record-view.md)
-   [テーブルの管理：一覧画面](../../../../../grid/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](table-management-choice-json.md)
-   [テーブルの管理：一覧画面：既定のビュー](../../../../../grid/table-management-default-view.md)
-   [テーブルの管理：エディタ：項目の詳細設定：検索機能を使う](../table-management-use-search.md)
