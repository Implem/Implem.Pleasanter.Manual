---
title: 状況項目の選択肢をカスタマイズしたい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-status-and-class-selections
translationKey: faq-status-and-class-selections
shortname: ''
created: 2020-02-05
updated: 2024-07-08
---

## 回答

[分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)項目と同様の操作で選択肢一覧の内容を変更してください。

---

## 前提条件

1.  コード値は数値で設定してください。
1.  コード値に[General.json](../../setup/parameters/general.json.md)の「CompletionCode」で設定した値以上の数値を設定するとその選択肢は完了とみなされます。
1.  設定するクラス名は"status-"で始まる必要があります。

## 概要

[状況](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目の内容は標準では以下の通りですが、自由にカスタマイズすることが可能です。

![状況項目の標準の選択肢が表示されている状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/4c94465b5ee94df99287cedbba081006.png)

## 操作手順

1.  対象となるテーブルを開きナビゲーションメニューより「管理」→[テーブルの管理](../../managers-guide/manage-table/index.md)をクリック

    ![ナビゲーションメニューからテーブルの管理を開くところ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/921d35f442d34d749cf3b7f48b3a1c67.png)

1.  [エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを開き[状況](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目を選択して「詳細設定」ボタンをクリック

    ![エディタタブで状況項目を選び「詳細設定」ボタンを押すところ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/523c4d842e2e47b3b7bc8a31c37819a0.png)

1.  [選択肢一覧](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)の内容を変更してください。

    ![詳細設定の選択肢一覧。状況の選択肢を書き換える](https://pleasanter.org/files/images/ja/FAQ/editor/assets/61b5feaaa4cd4ff98dcef316cb9da612.png)

1.  書式はカンマ区切りで以下の内容となります。

    ``` csv
    [データベースへ登録するコード値],[エディタ画面の表示],[一覧画面の表示],[スタイルシートのクラス名]
    ```

    "status-original-color"など新しいスタイルを作成し、[スタイル](../../developers-guide/style/index.md)に登録することで自由にスタイルを変更することが可能です。

    ``` css
    .status-original-color {
        color:red;
        background:yellow;
    }
    ```

## 関連情報

-   [テーブルの管理：項目：分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [パラメータ設定：General.json](../../setup/parameters/general.json.md)
-   [テーブルの管理：項目：状況](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードのエディタ画面](../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
