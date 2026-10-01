---
title: コピー時に子レコードを同時にコピーする
category: エディタ
order: '10600'
status: ''
parts: ''
urlstring: table-management-copy-with-links
translationKey: table-management-copy-with-links
shortname: コピー時に子レコードを同時にコピーする
created: 2021-09-26
updated: 2025-01-30
---

## 概要

[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)した[テーブル](../../../../../../../users-guide/table/index.md)の親レコードを[コピー](../../../../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)または[参照コピー](../../../../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)した際に関連する子「レコード」を同時に[コピー](../../../../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)することができます。[削除時に子レコードを同時に削除する](table-management-delete-with-links.md)と同時に設定することができます。

## 制限事項

-    [分類項目](../../../columns/table-management-class.md)のみ使用できます。

## 前提条件

-   設定を行うには「サイトの管理権限」が必要です。

## 操作手順

該当する分類項目の[選択肢一覧](index.md)にJSON形式で[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)を指定します。記述方法は「[テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](table-management-choice-json.md)」と同様です。

## 設定例1

下記の例ではサイトID 6 に[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)し、サイトID 6 の「レコード」を[コピー](../../../../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)した際に、関連する子「レコード」を自動的に[コピー](../../../../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)します。[タイトル](../../../../../../tenant-administration/tenant-logo.md)の末尾に " - copy"の文字を付与します。[コメント](../../../../../../../users-guide/common/comment.md)はコピーしません。

``` json title="選択肢一覧" linenums="1"
[
    {
        "SiteId": 6,
        "LinkActions": [
            {
                "Type": "CopyWithLinks",
                "CharToAddWhenCopying": " - copy",
                "CopyWithComments": false
            }
        ]
    }
]
```

## 設定内容

|No|選択肢|説明|
|:----|:----|:----|
|1|Type|"CopyWithLinks" を指定します。|
|2|CharToAddWhenCopying|[コピー時に追加する文字](../../../../characters-to-add-when-copying/index.md)を指定します。省略した場合には[テーブルの管理](../../../../../index.md)の設定が使用されます。|
|3|CopyWithComments|コメントをコピーするか true/false で指定します。省略した場合には false となります。|
|4|View: ColumnFilterHash|[JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)を使用して[コピー](../../../../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)対象を絞り込むことができます。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.5.0 以降|機能追加|

## 関連情報

-   [応用編：リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブル機能](../../../../../../../users-guide/table/index.md)
-   [応用編：コピーと参照コピー](../../../../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：削除時に子レコードを同時に削除する](table-management-delete-with-links.md)
-   [テーブルの管理：項目：分類](../../../columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](table-management-choices-text-depts.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](table-management-choice-json.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../../../../tenant-administration/tenant-logo.md)
-   [共通機能：コメントを追加](../../../../../../../users-guide/common/comment.md)
-   [テーブルの管理：エディタ：コピー時に追加する文字](../../../../characters-to-add-when-copying/index.md)
-   [テーブルの管理](../../../../../index.md)
-   [開発者ガイド：JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)