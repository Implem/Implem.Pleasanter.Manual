---
title: コピーと参照コピー
category: 操作ガイド（応用編）
order: '40'
status: ''
parts: ''
urlstring: advanced-operations-copy
translationKey: advanced-operations-copy
shortname: 応用編,コピー,参照コピー
created: 2023-07-26
updated: 2024-06-21
---

## 概要

レコードを複製するには「コピー」と「参照コピー」が利用できます。下記のような違いがありますので、ご要件に合わせて使い分けしてください。

| 項目                                                                                                                                              | コピー                                                       | 参照コピー                                                         |
| :------------------------------------------------------------------------------------------------------------------------------------------------ | :----------------------------------------------------------- | :----------------------------------------------------------------- |
| ボタンクリック時の挙動                                                                                                                            | コピー元のデータで新規作成し、作成した内容で編集画面が開く。 | コピー元のレコード内容がすべて記入された状態で新規作成画面を開く。 |
| 添付ファイル                                                                                                                                      | コピーできない                                               | コピーできない                                                     |
| 変更履歴                                                                                                                                          | コピーできない                                               | コピーできない                                                     |
| レコードのアクセス制御                                                                                                                            | コピーできない                                               | コピーできない                                                     |
| [既定値でコピー](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-copy-by-default.md)の項目 | コピー元の値は無視、既定値を設定                             | コピー元の値は無視、既定値を設定                                   |
| コメント                                                                                                                                          | コピーダイアログの「コメントをコピーする」の設定による       | コピーする                                                         |

### 必要な権限

「コピー」、「参照コピー」ともにレコードの「読取り」権限およびサイトの「作成」権限が必要です。

### 「コピー」、「参照コピー」の利用設定

[テーブルの管理](../../../managers-guide/manage-table/index.md)－[エディタ](../../table/record-authoring/edit-records/table-editor.md)で[コピーを許可](../../../managers-guide/manage-table/editor/allow-copy/index.md)または[参照コピーを許可](../../../managers-guide/manage-table/editor/allow-reference-copy/index.md)をチェックしてください。

![エディタタブの「コピーを許可」「参照コピーを許可」のチェック欄](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/ae05704ad0e741e6aadad8a7bf4399ee.png)

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：既定値でコピー](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-copy-by-default.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードのエディタ画面](../../table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エディタ：コピーを許可](../../../managers-guide/manage-table/editor/allow-copy/index.md)
-   [テーブルの管理：エディタ：参照コピーを許可](../../../managers-guide/manage-table/editor/allow-reference-copy/index.md)
