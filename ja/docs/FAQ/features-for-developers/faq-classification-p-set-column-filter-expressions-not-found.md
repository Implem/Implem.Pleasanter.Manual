---
title: ColumnFilterExpressionsを指定した分類項目に$p.setで値をセットすると「指定された情報は見つかりませんでした。」と表示される
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-classification-p-set-column-filter-expressions-not-found
translationKey: faq-classification-p-set-column-filter-expressions-not-found
shortname: ''
created: 2026-03-17
updated: 2026-03-23
---

## 回答

[検索機能を使う](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)がONの分類項目でColumnFilterExpressionsを使用している場合、$p.setで値をセットする際はColumnFilterExpressionsで指定した項目にも同時に値をセットしてください。

---

## 概要

### 発生条件

以下の条件がすべて揃ったときにエラーが発生します。

1. [分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)項目の[検索機能を使う](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)がON
1. [選択肢一覧](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)に[ColumnFilterExpressions](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json-column-filter-expressions.md)を用いたJSON形式で記述
1. [$p.set](../../developers-guide/script/update-site-info/script-set.md)で当該分類項目にのみ値をセットし、[ColumnFilterExpressions](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json-column-filter-expressions.md)で指定した項目には値をセットしない

### エラーメッセージ

```csv
指定された情報は見つかりませんでした。
```

### 原因

[ColumnFilterExpressions](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json-column-filter-expressions.md)は、別の項目に入力された値をもとにドロップダウンリストを生成する仕組みです。また[検索機能を使う](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)がONの場合、選択肢一覧から選択されたレコードを検索し、タイトルを取得して画面に表示する処理が実行されます。

このため、[ColumnFilterExpressions](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json-column-filter-expressions.md)で指定した項目に値が入っていない状態で[分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)項目に[$p.set](../../developers-guide/script/update-site-info/script-set.md)で値をセットすると、[選択肢一覧](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)が存在しない状態でタイトル取得の検索が実行されるため、エラーが表示されます。

### 対処方法

[$p.set](../../developers-guide/script/update-site-info/script-set.md)で分類項目に値をセットする際は、[ColumnFilterExpressions](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json-column-filter-expressions.md)で指定した項目にも同時に値をセットしてください。

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：検索機能を使う](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)
-   [テーブルの管理：項目：分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ（選択肢一覧を他の項目の値で絞り込む）](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json-column-filter-expressions.md)
-   [$p.set](../../developers-guide/script/update-site-info/script-set.md)