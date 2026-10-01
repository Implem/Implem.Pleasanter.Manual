---
title: サイトのタイトルを含める
category: 検索
order: '4000'
status: ''
parts: ''
urlstring: table-management-full-text-include-site-title
translationKey: table-management-full-text-include-site-title
shortname: サイトのタイトルを含める
created: 2021-05-30
updated: 2025-01-30
---

## 概要

サイトのタイトルで検索できるようにするには、オンにします。オンにするとサイトのタイトルが[フルテキストデータ](index.md)に保存されます。

## 制限事項

1.  本設定を変更した後は[検索インデックスの再構築](../table-management-rebuild-search-indexes.md)を実施するまで、既存のレコードの[フルテキストデータ](index.md)は古いままとなります。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 既定値

既定値は オン です。[Search.json](../../../../setup/parameters/search-json.md)の「FullTextIncludeSiteTitle」で変更可能です。

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.1.27.0 以降  | 機能追加 |

## 関連情報

-   [テーブルの管理：検索：フルテキストの設定](index.md)
-   [テーブルの管理：検索：操作：検索インデックスの再構築](../table-management-rebuild-search-indexes.md)
-   [パラメータ設定：Search.json](../../../../setup/parameters/search-json.md)
