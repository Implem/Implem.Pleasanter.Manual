---
title: リンク先テーブルの選択肢項目をフィルタに設定したが、選択肢が表示されない。
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-filter-option-not-displayed
translationKey: faq-filter-option-not-displayed
shortname: ''
created: 2024-08-21
updated: 2024-11-14
---

## 回答

[リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)しているテーブルの関係性や、リンク形式によって選択肢に表示されない場合があります。

---

## 概要

プリザンターはリンク先のテーブルの項目もフィルタとして利用することができますが、以下ケースの場合は選択肢が表示されませんので、回避方法の手順で表示させてください。

![フィルタに選択肢が表示されていない状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/f3884b8edaa044b39806b1833cb799ae.png)

### 1. 2段階以上先のテーブルをリンクした項目をフィルタに指定した場合

上図の構成において、「テーブル1」のフィルタに「テーブル3」の分類Bを設定すると選択肢が表示されません。
≪回避方法≫
「テーブル3」の分類Bにおいて[検索機能を使う](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)を有効にしてください。

### 2. 2段階以上先のテーブルをJSON形式でリンクした項目をフィルタに指定した場合

上図の構成において、「テーブル1」のフィルタに「テーブル4」の分類Cを設定すると選択肢が表示されません。
[表示フォーマット](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)の指定や[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)、[ルックアップ](../../users-guide/hands-on/advanced/advanced-operations-link.md)などの設定（JSON形式でリンク設定）した場合は[検索機能を使う](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)を有効にしても選択肢が表示されません。

≪回避方法≫
JSON形式での選択肢設定から角括弧二重のリンク設定に変更してください。

## 関連情報

-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：エディタ：項目の詳細設定：検索機能を使う](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)