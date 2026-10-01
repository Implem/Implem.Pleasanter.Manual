---
title: 項目連携を使用する
category: フィルタ
order: '1500'
status: ''
parts: ''
urlstring: table-management-filter-column-relation
translationKey: table-management-filter-column-relation
shortname: 項目連携
created: 2020-01-20
updated: 2024-06-03
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)の[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)の[分類項目](../editor/editor-settings/columns/table-management-class.md)間に親子関係を設定することができます。[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)の分類Aが都道府県、分類Bが市町村であった場合、[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)の分類Aで東京都を選択した際に分類Bで東京都内の市区町村のみを表示する、といった連携が可能となります。

##### サンプルデータ

```
- 東京都
   - 杉並区
   - 渋谷区
   - 港区
   - 中央区
   - 千代田区
   - 新宿区
   - 中野区

- 神奈川県
   - 厚木市
   - 相模原市
   - 逗子市
   - 鎌倉市
   - 横須賀市
   - 川崎市
   - 横浜市
```

## 制限事項

1. [一覧のヘッダメニューでフィルタを使用する](table-management-filter-use-grid-header-filters.md)と「項目連携を使用する」を同時に「オン」にすることはできません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。
1. 本設定は[分類項目](../editor/editor-settings/columns/table-management-class.md)の[項目連携](../editor/relating-column-settings/index.md)が完了していることを前提としており、[項目連携](../editor/relating-column-settings/index.md)を[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)上の[項目](../editor/editor-settings/columns/index.md)にも適用するための設定です。

## 操作手順

1. テーブルの管理を選択し、フィルタタブをクリックしてください。  
2. 画面下の「項目連携を使用する」を選択してください。  
（「項目連携を使用する」と[一覧のヘッダメニューでフィルタを使用する](table-management-filter-use-grid-header-filters.md)を同時に有効にすることはできません。）  
![フィルタタブの下部にある「項目連携を使用する」の設定](https://pleasanter.org/files/images/ja/managers-guide/manage-table/filter/assets/d1bb71450c4b4a37bf0a8e56b0da6ba7.png)

3. 画面下の「更新」ボタンを押し、一覧画面に戻ってください。  
4. フィルタ上で「都道府県」を選択すると、選択した内容に応じて「市区町村」には絞り込まれたデータのみが表示されることを確認してください。  
![一覧画面のフィルタで「都道府県」を選択したところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/filter/assets/b0126cd99a7b44c281bdbf3e5090f489.png) 
![「都道府県」の選択に応じて「市区町村」が絞り込まれたフィルタ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/filter/assets/5b5b867b2b114c9b9595c89031b88eef.png)

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：項目：分類](../editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：フィルタ：一覧のヘッダメニューでフィルタを使用する](table-management-filter-use-grid-header-filters.md)
-   [テーブルの管理：エディタ：項目連携](../editor/relating-column-settings/index.md)
-   [テーブルの管理：項目](../editor/editor-settings/columns/index.md)