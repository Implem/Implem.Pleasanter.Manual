---
title: 横断検索
category: 共通機能
order: '5'
status: ''
parts: ''
urlstring: crosssearch
translationKey: crosssearch
shortname: 横断検索
created: 2024-04-23
updated: 2024-11-25
---

## 概要

プリザンターの全レコードに対して指定したキーワードで検索を行います。横断検索は[フルテキスト検索](../../FAQ/others/faq-search.md)となります。

## 制限事項

1. 「読取り権限」がないテーブル、レコードは検索できません。
1. [Search.json](../../setup/parameters/search-json.md)の「DisableCrossSearch」がtrueの場合、横断検索機能が使用できません。横断検索テキストボックスが非表示になります。
1. [テーブルの管理](../../managers-guide/manage-table/index.md)－[検索](../../managers-guide/manage-table/search/index.md)で[横断検索を無効化](../../managers-guide/manage-table/search/table-management-disable-cross-search.md)にチェックしているテーブルは検索対象外となります。

## 操作手順

1. 画面右上の横断検索テキストボックスに検索したいキーワードを入力し、エンターキーを押下します。
![キーワードを入力した横断検索のテキストボックス](https://pleasanter.org/files/images/ja/users-guide/common/assets/7caf5074973540f9b0679bbcf7b6a151.png)

1. 検索結果が表示されます。検索文字列は黄色のハイライトで表示されます。
![検索文字列が黄色くハイライトされた横断検索の結果画面](https://pleasanter.org/files/images/ja/users-guide/common/assets/6c1b144f0b5b44eebc9417bc4f4ffb9b.png)
  ただし検索文字列が複数（and検索）の場合はハイライト表示しません。
![検索文字列が複数のときの、ハイライトされない横断検索の結果画面](https://pleasanter.org/files/images/ja/users-guide/common/assets/f1720e698ab944b7907586fec7306a4f.png)

1. 検索結果のレコードをクリックすると該当レコードの編集画面に遷移します。検索結果のレコード内のパンくずリストをクリックするとクリックしたサイトに遷移します。

## 関連情報

-   [FAQ：検索にヒットしない](../../FAQ/others/faq-search.md)
-   [パラメータ設定：Search.json](../../setup/parameters/search-json.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [テーブルの管理：検索](../../managers-guide/manage-table/search/index.md)
-   [テーブルの管理：検索：検索の設定：横断検索を無効化](../../managers-guide/manage-table/search/table-management-disable-cross-search.md)
