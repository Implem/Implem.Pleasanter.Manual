---
title: 一覧表示でチェックボックスが表示されず一括更新、一括削除が使えない
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-grid-checkbox-not-show
translationKey: faq-grid-checkbox-not-show
shortname: ''
created: 2021-03-03
updated: 2024-07-01
---

## 回答

[一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)で子テーブルの項目を表示しているためです。

---

## 概要

テーブルのリンク機能でテーブルの親子関係を結んでいる場合、親テーブルで子テーブルの項目を一覧表示している場合には、左列のチェックボックスは表示されないため、[一括更新](../../users-guide/table/record-authoring/edit-records/table-record-bulkupdate.md)、[一括削除](../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)を行うことはできません。
レコードを誤って削除してしまうといった誤操作を防ぐため、このような仕様となっております。

通常であれば一覧表示の左列にはチェックボックスが表示されます。  
![通常の一覧画面。左列にチェックボックスが表示されている](https://pleasanter.org/files/images/ja/FAQ/grid/assets/7411efa7d91a458eace88177a840adfd.png) 

以下のように、親テーブルの一覧で子テーブルの項目を有効化している場合は、一覧表示でチェックボックスが表示されません。   
![親テーブルの一覧タブで子テーブルの項目を有効化した設定](https://pleasanter.org/files/images/ja/FAQ/grid/assets/4e78106d4cf0434c9bc09903326af656.png)

親テーブルのレコードが複数行表示されるため、誤操作防止のための仕様となります。  
![親テーブルのレコードが複数行表示され、チェックボックスがない一覧画面](https://pleasanter.org/files/images/ja/FAQ/grid/assets/549ba5d9a8164429912989e519bc7500.png)

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブル機能：レコードの一括更新](../../users-guide/table/record-authoring/edit-records/table-record-bulkupdate.md)
-   [テーブル機能：レコードの一括削除](../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)