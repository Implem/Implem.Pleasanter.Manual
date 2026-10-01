---
title: カスタムデザインを使用
category: 一覧画面
order: '70'
status: ''
parts: ''
urlstring: table-management-use-grid-design
translationKey: table-management-use-grid-design
shortname: カスタムデザインを使用
created: 2021-05-06
updated: 2025-09-19
---

## 概要

[一覧画面](../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)上の「セル」に複数の項目を表示する場合に使用します。[管理者項目](../../editor/editor-settings/columns/table-management-manager.md)と[担当者項目](../../editor/editor-settings/columns/table-management-owner.md)を1つの「セル」に表示して「一覧表」の幅を減らしたい場合などに使用します。[マークダウン](../../../../users-guide/common/markdown.md)が使用可能です。

## 制限事項

1. 「カスタムデザイン」を使用した項目は[一覧編集](../../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)で編集できません。
1. 他の[テーブル](../../../../users-guide/table/index.md)の[項目](../../editor/editor-settings/columns/index.md)は「カスタムデザイン」に使用できません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 操作方法

1. [一覧画面の項目の詳細設定](index.md)を参照してください。

## 設定例

下記は[管理者項目](../../editor/editor-settings/columns/table-management-manager.md)と「担当者」項目を1つの「セル」に表示する例です。

##### Text

```
[管理者]
[担当者]
```

## 動作イメージ

下図の例では「カスタムデザイン」に加え[一覧画面](../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)上のヘッダを変更するために[一覧画面の表示名](table-management-grid-label-text.md)に「管理者/担当者」を設定しています。
![カスタムデザインで管理者と担当者を1つの列にまとめた一覧画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/8eab0cdc80584b5db6a554b6d4958e3c.png)

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理：項目：管理者](../../editor/editor-settings/columns/table-management-manager.md)
-   [テーブルの管理：項目：担当者](../../editor/editor-settings/columns/table-management-owner.md)
-   [共通機能：マークダウン](../../../../users-guide/common/markdown.md)
-   [テーブル機能：レコードの一覧編集](../../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)
-   [テーブル機能](../../../../users-guide/table/index.md)
-   [テーブルの管理：項目](../../editor/editor-settings/columns/index.md)
-   [テーブルの管理：一覧画面：項目の詳細設定](index.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：一覧画面の表示名](table-management-grid-label-text.md)