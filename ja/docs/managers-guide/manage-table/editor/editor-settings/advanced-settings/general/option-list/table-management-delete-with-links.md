---
title: 削除時に子レコードを同時に削除する
category: エディタ
order: '10700'
status: ''
parts: ''
urlstring: table-management-delete-with-links
translationKey: table-management-delete-with-links
shortname: 削除時に子レコードを同時に削除する
created: 2021-09-26
updated: 2025-05-13
---

## 概要

[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)した[テーブル](../../../../../../../users-guide/table/index.md)の親レコードを[削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)または[一括削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)した際に関連する子「レコード」を同時に[削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)することができます。[コピー時に子レコードを同時にコピーする](table-management-copy-with-links.md)と同時に設定することができます。

## 制限事項

-   [分類項目](../../../columns/table-management-class.md)のみ使用できます。

## 前提条件

-   設定を行うには「サイトの管理権限」が必要です。

## 操作手順

該当する分類項目の[選択肢一覧](index.md)にJSON形式で[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)を指定します。記述方法は「[テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](table-management-choice-json.md)」と同様です。

## 設定例

下記の例ではサイトID 6に[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)し、サイトID 6の「レコード」を[削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)または[一括削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)した際に、関連する子「レコード」を自動的に[削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)します。

``` json title="選択肢一覧" linenums="1"
[
    {
        "SiteId": 6,
        "LinkActions": [
            {
                "Type": "DeleteWithLinks"
            }
        ]
    }
]
```

## 設定内容

|No|選択肢|説明|
|:----|:----|:----|
|1|Type|"DeleteWithLinks" を指定します。|
|2|View: ColumnFilterHash|[JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)を使用して[削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)対象を絞り込むことができます。|

## [一括削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)との関係

テーブルの分類項目の[選択肢一覧](index.md)に「削除時に子レコードを同時に削除する」設定を行っている場合、親レコードの削除と連動して子レコードが削除される際は、子レコードが登録されているテーブルに対して[一括削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)の処理が実行されます。したがって、子レコードが登録されているテーブルに、[条件](../../../../../../../FAQ/editor/faq-condition-mode-range.md)に「一括削除前」、「一括削除後」を指定したサーバスクリプトが登録されている場合、該当のサーバスクリプトが実行されます。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.5.0 以降|機能追加|
|1.4.16.0 以降|サーバスクリプトの条件「一括削除前」、「一括削除後」の追加に伴い、[一括削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)との関係についてを追記|

## 関連情報

-   [応用編：リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブル機能](../../../../../../../users-guide/table/index.md)
-   [テーブル機能：レコードの削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)
-   [テーブル機能：レコードの一括削除](../../../../../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：コピー時に子レコードを同時にコピーする](table-management-copy-with-links.md)
-   [テーブルの管理：項目：分類](../../../columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](table-management-choices-text-depts.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](table-management-choice-json.md)
-   [開発者ガイド：JSONデータレイアウト：View](../../../../../../../developers-guide/json-data-layout/api-view/index.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../../../../../FAQ/editor/faq-condition-mode-range.md)