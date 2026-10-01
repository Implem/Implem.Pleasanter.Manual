---
title: Search.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: search-json
translationKey: search-json
shortname: Search.json
created: 2019-04-30
updated: 2024-12-12
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 制限事項

1. SearchDocuments: trueの場合に使用するiFilterはSQL Serverのオプション機能です。PostgreSQLの環境では使用できません。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|SearchDocuments|true|本パラメータをtrueに設定し、ファイルの種類に合ったIFilterをインストールすると添付ファイル内部の検索が行えます。|
|CreateIndexes|true|trueに設定した場合、レコード更新時に検索インデックスの作成を行います。**本パラメータはtrue以外に設定しないでください。**|
|PageSize|20|検索結果を一度に取得するレコードの上限を指定。|
|DisableCrossSearch|false|横断検索を無効化する場合、trueを指定。なお、テーブルごとに無効化設定したい場合は、[横断検索を無効化](../../managers-guide/manage-table/search/table-management-disable-cross-search.md)を参照。|
|DisableCrossSearchSites|false|[横断検索](../../users-guide/common/crosssearch.md)の結果に[サイト](../../users-guide/site/index.md)を含めない場合にはtrueを指定。|
|FullTextIncludeBreadcrumb|false|[フルテキストデータ](../../managers-guide/manage-table/search/fulltext-settings/index.md)に[パンくずリストを含める](../../managers-guide/manage-table/search/fulltext-settings/table-management-full-text-include-breadcrumb.md)を既定値にする場合にはtrueを指定。|
|FullTextIncludeSiteId|false|[フルテキストデータ](../../managers-guide/manage-table/search/fulltext-settings/index.md)に[サイトIDを含める](../../managers-guide/manage-table/search/fulltext-settings/table-management-full-text-include-site-id.md)を既定値にする場合にはtrueを指定。|
|FullTextIncludeSiteTitle|false|[フルテキストデータ](../../managers-guide/manage-table/search/fulltext-settings/index.md)に[サイトのタイトルを含める](../../managers-guide/manage-table/search/fulltext-settings/table-management-full-text-include-site-title.md)を既定値にする場合にはtrueを指定。|
|FullTextNumberOfMails|10|[フルテキストデータ](../../managers-guide/manage-table/search/fulltext-settings/index.md)に含める[メールの件数](../../managers-guide/manage-table/search/fulltext-settings/table-management-full-text-number-of-mails.md)の既定値を指定。|
|FullTextMaxNumberOfMails|100|[フルテキストデータ](../../managers-guide/manage-table/search/fulltext-settings/index.md)に含める[メールの件数](../../managers-guide/manage-table/search/fulltext-settings/table-management-full-text-number-of-mails.md)の最大値を指定。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.27.0 以降|FullTextIncludeBreadcrumbを追加<br>FullTextIncludeSiteIdを追加<br>FullTextIncludeSiteTitleを追加<br>FullTextNumberOfMailsを追加<br>FullTextMaxNumberOfMailsを追加|
|1.2.4.0 以降|DisableCrossSearchを追加|
|1.2.15.0 以降|DisableCrossSearchSitesを追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [テーブルの管理：検索：検索の設定：横断検索を無効化](../../managers-guide/manage-table/search/table-management-disable-cross-search.md)
-   [共通機能：横断検索](../../users-guide/common/crosssearch.md)
-   [サイト機能](../../users-guide/site/index.md)
-   [テーブルの管理：検索：フルテキストの設定](../../managers-guide/manage-table/search/fulltext-settings/index.md)
-   [テーブルの管理：検索：フルテキストの設定：パンくずリストを含める](../../managers-guide/manage-table/search/fulltext-settings/table-management-full-text-include-breadcrumb.md)
-   [テーブルの管理：検索：フルテキストの設定：サイトIDを含める](../../managers-guide/manage-table/search/fulltext-settings/table-management-full-text-include-site-id.md)
-   [テーブルの管理：検索：フルテキストの設定：サイトのタイトルを含める](../../managers-guide/manage-table/search/fulltext-settings/table-management-full-text-include-site-title.md)
-   [テーブルの管理：検索：フルテキストの設定：メールの件数](../../managers-guide/manage-table/search/fulltext-settings/table-management-full-text-number-of-mails.md)
