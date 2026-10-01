---
title: columns.ClearChoiceHash
icon: material/alpha-m-box
category: サーバスクリプト
order: '6015'
status: ''
parts: ''
urlstring: server-script-columns-clear-choice-hash
translationKey: server-script-columns-clear-choice-hash
shortname: columns.ClearChoiceHash
created: 2021-10-17
updated: 2023-06-21
---

## 概要

[columns](index.md)オブジェクト」の「ClearChoiceHashメソッド」です。[サーバスクリプト](../index.md)で[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)をクリアします。

## 制限事項

1. [分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)のみ使用できます。
1. サーバスクリプトの[条件](../../../FAQ/editor/faq-condition-mode-range.md)が「画面表示の前」、「行表示の前」の場合に有効となります。

## 前提条件

1. 対象となる[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の選択肢一覧に、選択肢が1つ以上設定されている必要があります。

## 構文

```javascript
columns.[カラム名].ClearChoiceHash();
```

## パラメータ

パラメータはありません。

## 戻り値

戻り値はありません。

## 使用例

下記の例では[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)の選択肢をクリアしています。

##### JavaScript

```javascript
columns.ClassA.ClearChoiceHash();
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
