---
title: 既存の分類で複数選択を有効にすると登録済みデータが未選択状態になる
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-class-single-data-to-multiple-data
translationKey: faq-class-single-data-to-multiple-data
shortname: ''
created: 2021-03-10
updated: 2025-01-30
---

## 回答

レコードを[エクスポート](../../developers-guide/api/table-operations/api-export.md)し、「キーが一致するレコードを更新する」を必ずチェックして[インポート](../../users-guide/table/record-authoring/create-records/table-record-import.md)します。

---

## 概要

新規に追加した分類ではなく、登録済みのデータが存在している分類で[複数選択](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)を有効にすると、データの保存形式が変更されるため編集画面では正しく表示されません。

下図では「参加者」が「[複数選択](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)」を有効化した分類項目です。一覧画面の1行目と2行目は複数選択の有効化後に作成したレコードです。一覧画面の3行目は複数選択の有効化前に作成したレコードです。

=== "一覧画面"

    データ自体は正常に保存されているため、正しく表示されます。

    ![一覧画面。複数選択の有効化前に作成したレコードでも参加者が正しく表示されている](https://pleasanter.org/files/images/ja/FAQ/editor/assets/ae71f1f5068149a5b06bfd22e83d5262.png)

=== "編集画面"

    未選択状態で表示されます。

    ![編集画面。複数選択の有効化前に作成したレコードで参加者が未選択になっている](https://pleasanter.org/files/images/ja/FAQ/editor/assets/f0bf93d7b1024224be8c3f0d6a057efa.png)

## 操作手順

正しく表示させるためには、以下の手順でデータの保存形式を変換してください。

1.  「[一覧](../../users-guide/table/record-authoring/data-analysis/table-grid.md)」画面でデータをエクスポートしてください。この際、エクスポートする項目として対象の分類を必ず含めてください。通常は「[テーブルの管理](../../managers-guide/manage-table/index.md)」画面の「[一覧](../../managers-guide/manage-table/grid/index.md)」タブまたは「[エディタ](../../managers-guide/manage-table/editor/index.md)」タブで有効化された項目が出力されます。
1.  エクスポートしたファイルをインポートしてください。この際、インポートダイアログの「キーが一致するレコードを更新する」のチェックをオンにして、「[インポート](../../users-guide/table/record-authoring/create-records/table-record-import.md)」ボタンをクリックしてください。

    ![インポートダイアログ。「キーが一致するレコードを更新する」にチェックが入っている](https://pleasanter.org/files/images/ja/FAQ/editor/assets/d881a8519c744ef0a46dcb41b37f1ac6.png)

1.  インポート完了後は、複数選択の有効化前に作成したレコードでも、正常に選択された状態で表示されます。

    ![インポート後の編集画面。参加者が選択された状態で表示されている](https://pleasanter.org/files/images/ja/FAQ/editor/assets/ae729c73e43c4d6596f38e1fad014853.png)

## 関連情報

-   [開発者ガイド：API：テーブル操作：テーブルのエクスポート](../../developers-guide/api/table-operations/api-export.md)
-   [組織管理機能：インポート](../../managers-guide/department-administration/dept-import.md)
-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)
