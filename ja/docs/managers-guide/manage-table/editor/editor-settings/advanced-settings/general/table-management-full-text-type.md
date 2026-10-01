---
title: フルテキストの種類
category: エディタ
order: '13500'
status: ''
parts: ''
urlstring: table-management-full-text-type
translationKey: table-management-full-text-type
shortname: フルテキストの種類
created: 2021-05-05
updated: 2023-04-27
---

## 概要

[検索](../../../../search/index.md)で使用する[フルテキストデータ](../../../../search/fulltext-settings/index.md)に保存する文字列の種類の設定です。本設定の変更後は[検索インデックスの再構築](../../../../search/table-management-rebuild-search-indexes.md)を行う必要があります。

## 注意事項

1.  [フルテキストデータ](../../../../search/fulltext-settings/index.md)の文字量が多すぎる場合、[検索](../../../../search/index.md)が遅くなることがあります。[説明項目](../../columns/table-management-description.md)など多くのテキストが含まれる「入力項目」で「無し」以外を設定する場合には、文字列の量に注意する必要があります。

## 制限事項

1.  本設定を変更した後は[検索インデックスの再構築](../../../../search/table-management-rebuild-search-indexes.md)を実施するまで、既存のレコードの[フルテキストデータ](../../../../search/fulltext-settings/index.md)は古いままとなります。
1.  [状況項目](../../columns/table-management-status.md)、[管理者項目](../../columns/table-management-manager.md)、[担当者項目](../../columns/table-management-owner.md)、[分類項目](../../columns/table-management-class.md)など値と表示名が異なる場合以外は、「値」、[表示名](table-management-label-text.md)、「値と表示名」の何れを選択しても同じ文字列が[フルテキストデータ](../../../../search/fulltext-settings/index.md)に保存されます。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 設定内容

| No  | 選択肢     | 説明                                                 |
| :-- | :--------- | :--------------------------------------------------- |
| 1   | 無し       | 検索にヒットしないよう何も保存しません。             |
| 2   | 表示名     | 表示名で検索が行えるよう表示名を保存します。         |
| 3   | 値         | 値で検索が行えるよう値を保存します。                 |
| 4   | 値と表示名 | 値と表示名で検索が行えるよう値と表示名を保存します。 |

## 関連情報

-   [テーブルの管理：検索](../../../../search/index.md)
-   [テーブルの管理：検索：フルテキストの設定](../../../../search/fulltext-settings/index.md)
-   [テーブルの管理：検索：操作：検索インデックスの再構築](../../../../search/table-management-rebuild-search-indexes.md)
-   [テーブルの管理：項目：説明](../../columns/table-management-description.md)
-   [テーブルの管理：項目：状況](../../columns/table-management-status.md)
-   [テーブルの管理：項目：管理者](../../columns/table-management-manager.md)
-   [テーブルの管理：項目：担当者](../../columns/table-management-owner.md)
-   [テーブルの管理：項目：分類](../../columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](table-management-label-text.md)
