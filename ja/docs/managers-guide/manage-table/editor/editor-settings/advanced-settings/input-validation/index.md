---
title: 入力検証
category: エディタ
order: '16500'
status: ''
parts: ''
urlstring: table-management-validation
translationKey: table-management-validation
shortname: 入力検証
created: 2020-06-11
updated: 2024-04-09
---

## 概要

「入力項目」の内容を「正規表現」で検証するための設定です。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 操作手順

入力検証を設定したいテーブルを開き「管理」→[テーブルの管理](../../../../index.md)→[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)を開き、設定したい項目を選択して「詳細設定」をクリックしてください。

対象となる項目は、[タイトル](../../../../../tenant-administration/tenant-logo.md)、[内容](../../columns/table-management-body.md)、[分類](../../columns/table-management-class.md)、[説明](../general/table-management-column-description.md)、[コメント](../../../../../../users-guide/common/comment.md)となります。

![エディタタブで項目を選び「詳細設定」を押す画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/input-validation/assets/3961db0a8c2c4930a4bb64fe47a8a85d.png)

「入力検証」タブを開いてください。  

| 項目名               | 内容                                                                                                       |
| -------------------- | ---------------------------------------------------------------------------------------------------------- |
| クライアント正規表現 | 入力後に、項目からフォーカスが移ったタイミングで内容を検証します。後読みなど一部のパターンは使用できません |
| サーバ正規表現       | レコードの作成・更新のタイミングで内容を検証します                                                         |
| エラーメッセージ     | 入力内容にエラーが発生した場合に表示されるメッセージを指定します                                           |

![項目の詳細設定の「入力検証」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/input-validation/assets/e082e738ff8b446f8d6cb97a068964c5.png)

## 使用例

以下の正規表現とエラーメッセージで、携帯電話番号の入力を検証します。項目には123456789を入力します。

### 正規表現

``` text
^0[789]0\d{8}$
```

### エラーメッセージ

``` text
携帯電話番号の入力に誤りがあります。
```

### クライアント正規表現

クライアント正規表現に上記の正規表現を設定して、実際の入力画面でエラーが発生した場合、以下のように項目下部にメッセージを表示します。

![クライアント正規表現のエラーが項目の下に表示された画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/input-validation/assets/e1eb77adbaf44b55bfe950b5b8c84999.png)

### サーバ正規表現

サーバ正規表現に上記の正規表現を設定して、実際の入力画面でエラーが発生した場合、以下のように画面下部にメッセージを表示します。

![サーバ正規表現のエラーが画面下部に表示された画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/input-validation/assets/e1b5f184e7ad4930bea46934a7988742.png)

## 関連情報

-   [テーブルの管理](../../../../index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../../../tenant-administration/tenant-logo.md)
-   [テーブルの管理：項目：内容](../../columns/table-management-body.md)
-   [テーブルの管理：項目：分類](../../columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../general/table-management-column-description.md)
-   [共通機能：コメントを追加](../../../../../../users-guide/common/comment.md)
