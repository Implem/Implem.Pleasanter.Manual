---
title: 状況項目の値により進捗率を自動で指定する
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-automatic-entry-of-progress-rate
translationKey: faq-automatic-entry-of-progress-rate
shortname: FAQ：状況項目の値により進捗率を自動で指定する
created: 2020-12-15
updated: 2026-03-25
---

## 回答

[サーバスクリプト](../../developers-guide/server-script/index.md)を使用してください。

---

## 概要

編集画面および一覧画面の一括編集モードで[状況](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目に選択された値によって進捗率を自動で指定するには[サーバスクリプト](../../developers-guide/server-script/index.md)を使用します。

サンプルコードでは、[状況](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目に割り当てられたコードに応じて、下表のとおり進捗率を指定しています。

|   コード | 選択肢   | 進捗率 |
| -------: | :------- | -----: |
|      150 | 準備     |    10% |
|      200 | 実施中   |    50% |
|      300 | レビュー |    90% |
|      900 | 完了     |   100% |
| (未選択) | その他   |     0% |

## 操作方法

1. 「期限付きテーブル」を作成してください。
1.  [状況](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目と[進捗率](../../users-guide/table/record-authoring/edit-records/table-record-progression-rate.md)項目を[エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)画面と[一覧](../../managers-guide/manage-table/grid/index.md)画面でそれぞれ有効化します [^1]。
1.  以下の[サーバスクリプト](../../developers-guide/server-script/index.md)を「新規作成」してください。  
    [条件](faq-condition-mode-range.md)は「計算式の後」を選択してください。

    ``` js title="「条件」は「計算式の後」" linenums="1"
    switch (model.Status) {
        case 150: // 準備
            model.ProgressRate = 10;
            break;
        case 200: // 実施中
            model.ProgressRate = 50;
            break;
        case 300: // レビュー
            model.ProgressRate = 90;
            break;
        case 900: // 完了
            model.ProgressRate = 100;
            break;
        default:  // その他
            model.ProgressRate = 0;
            break;
    }
    ```

[^1]: 期限付きテーブルを新規作成した場合は、デフォルトで有効化されています。

## 関連情報

-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
-   [テーブルの管理：項目：状況](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
-   [テーブル機能：レコードの進捗率表示](../../users-guide/table/record-authoring/edit-records/table-record-progression-rate.md)
-   [テーブル機能：レコードのエディタ画面](../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：一覧画面](../../managers-guide/manage-table/grid/index.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](faq-condition-mode-range.md)
