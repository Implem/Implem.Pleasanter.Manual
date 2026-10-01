---
title: メールの件数
category: 検索
order: '5000'
status: ''
parts: ''
urlstring: table-management-full-text-number-of-mails
translationKey: table-management-full-text-number-of-mails
shortname: メールの件数
created: 2021-05-30
updated: 2025-01-30
---

## 概要

レコードから送信したメールの内容を[フルテキストデータ](index.md)に含める件数を設定します。設定値を10とした場合、最新のメール10件の内容を[フルテキストデータ](index.md)に含めます。

## 制限事項

1.  設定可能な範囲は0～100の間です。設定可能な範囲を変更するには[Search.json](../../../../setup/parameters/search-json.md)の「FullTextMaxNumberOfMails」を変更する必要があります。
1.  本設定を変更した後は[検索インデックスの再構築](../table-management-rebuild-search-indexes.md)を実施するまで、既存のレコードの[フルテキストデータ](index.md)は古いままとなります。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 既定値

既定値は10です。[Search.json](../../../../setup/parameters/search-json.md)の「FullTextNumberOfMails」で変更可能です。

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.1.27.0 以降  | 機能追加 |

## 関連情報

-   [テーブルの管理：検索：フルテキストの設定](index.md)
-   [パラメータ設定：Search.json](../../../../setup/parameters/search-json.md)
-   [テーブルの管理：検索：操作：検索インデックスの再構築](../table-management-rebuild-search-indexes.md)
