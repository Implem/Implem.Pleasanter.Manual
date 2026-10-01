---
title: Item
category: JSONデータレイアウト
order: '2100'
status: ''
parts: ''
urlstring: api-item
translationKey: api-item
shortname: JSONデータレイアウト：Item
created: 2020-02-13
updated: 2026-07-14
---

## 概要

[API](../api/basics/api.md)の[レコード取得API](../api/table-operations/api-record-get-multi.md)を使用して取得する[テーブル](../../users-guide/table/index.md)の「レコード」のJSONデータのレイアウトについて説明します。

## JSONデータのレイアウト

|No|プロパティ名|項目名|データ型|備考|
|:----|:----|:----|:----|:----|
|1|SiteId|「サイトID項目」|long| |
|2|UpdatedTime|[更新日時項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updated-time.md)|DateTime| |
|3|IssueIdまたはResultId|[ID項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-id.md)|long| |
|4|Ver|[バージョン項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-ver.md)|int| |
|5|Title|[タイトル項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)|string| |
|6|Body|[内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)|string| |
|7|StartTime|[開始項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-start-time.md)|DateTime|期限付きテーブルのみ|
|8|CompletionTime|[完了項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)|DateTime|期限付きテーブルのみ|
|9|WorkValue|[作業量項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-work-value.md)|decimal|期限付きテーブルのみ|
|10|ProgressRate|[進捗率項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-progress-rate.md)|decimal|期限付きテーブルのみ|
|11|RemainingWorkValue|[残作業量項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-remaining-work-value.md)|decimal|期限付きテーブルのみ|
|12|Status|[状況項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)|int| |
|13|Manager|[管理者項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)|int| |
|14|Owner|[担当者項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)|int| |
|15|Locked|[ロック項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-lock.md)|bool| |
|16|Comments|[コメント項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)|string| |
|17|Creator|[作成者項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-creator.md)|int|ユーザID|
|18|Updator|[更新者項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updator.md)|int|ユーザID|
|19|CreatedTime|[作成日時項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-created-time.md)|DateTime| |
|20|ItemTitle|[タイトル項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)|string| |
|21|ClassHash|[分類項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)|Dictionary<string, string>|後述の設定例を参照|
|22|NumHash|[数値項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)|Dictionary<string, decimal>|後述の設定例を参照|
|23|DateHash|[日付項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)|Dictionary<string, DateTime>|後述の設定例を参照|
|24|DescriptionHash|[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)|Dictionary<string, string>|後述の設定例を参照|
|25|CheckHash|[チェック項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)|Dictionary<string, bool>|後述の設定例を参照|
|26|AttachmentsHash|[添付ファイル項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)|Dictionary<string, Attachments>|後述の「Attachmentsオブジェクト」および設定例を参照|

### Attachments オブジェクト

|プロパティ名|データ型|備考|
|--|--|--|
|Guid|文字列|添付ファイルのGUID|
|Name|文字列|添付ファイル名|
|ContentType|文字列|Content Type|
|Base64|文字列|ファイルデータをBase64エンコーディングしたもの|

## 設定例

ClassHash、NumHash、DateHash、DescriptionHash、CheckHashの設定例(json)
```
"ClassHash": {
    "ClassA": "分類",
    "ClassB": "未分類",
    "ClassC": "その他"
},
"NumHash": {
    "NumA": 100,
    "NumB": 200
},
"DateHash": {
    "DateA": "2019/01/01",
    "DateB": "2020/01/01"
},
"DescriptionHash": {
    "DescriptionA": "説明",
    "DescriptionB": "概要",
    "DescriptionC": "補足"
},
"CheckHash": {
    "CheckA": true,
    "CheckB": false
}
```

AttachmentsHashの設定例(json)
```
AttachmentsHash: {
    AttachmentsA: [
        {
            ContentType: 'text/plain',
            Name: 'Readme.txt',
        　  Base64: '5yY5Trfi4…'
        },
        {
            ContentType": 'text/csv',
            Name: 'data.csv',
        　  Base64: 'Rgfc2g3ZSe…'
        }
    ],
    AttachmentsB: [
        {
            ContentType: 'image/jpeg',
            Name: 'logo.jpeg',
        　  Base64: 'b4yT5HJfg2…'
        }
    ]
}
```

## 関連情報

-   [開発者ガイド：API](../api/basics/api.md)
-   [開発者ガイド：API：テーブル操作：複数レコード取得](../api/table-operations/api-record-get-multi.md)
-   [テーブル機能](../../users-guide/table/index.md)
-   [テーブルの管理：項目：更新日時](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updated-time.md)
-   [テーブルの管理：項目：ID](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-id.md)
-   [テーブルの管理：項目：バージョン](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-ver.md)
-   [テーブルの管理：項目：タイトル](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)
-   [テーブルの管理：項目：内容](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
-   [テーブルの管理：項目：開始](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-start-time.md)
-   [テーブルの管理：項目：完了](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)
-   [テーブルの管理：項目：作業量](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-work-value.md)
-   [テーブルの管理：項目：進捗率](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-progress-rate.md)
-   [テーブルの管理：項目：残作業量](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-remaining-work-value.md)
-   [テーブルの管理：項目：状況](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
-   [テーブルの管理：項目：管理者](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)
-   [テーブルの管理：項目：担当者](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)
-   [テーブルの管理：項目：ロック](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-lock.md)
-   [テーブルの管理：項目：コメント](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)
-   [テーブルの管理：項目：作成者](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-creator.md)
-   [テーブルの管理：項目：更新者](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updator.md)
-   [テーブルの管理：項目：作成日時](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-created-time.md)
-   [テーブルの管理：項目：分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)