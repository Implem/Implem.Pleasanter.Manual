---
title: コントロール種別(分類)
category: エディタ
order: '6800'
status: ''
parts: ''
urlstring: table-management-control-type-class
translationKey: table-management-control-type-class
shortname: コントロール種別(分類)
created: 2023-01-20
updated: 2024-04-09
---

## 概要

[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)上の[分類項目](../../columns/table-management-class.md)のコントロール種別を設定します。

## 制限事項

1. [分類項目](../../columns/table-management-class.md)、[状況項目](../../columns/table-management-status.md)、[管理者項目](../../columns/table-management-manager.md)、[担当者項目](../../columns/table-management-owner.md)でのみ設定できます。
1. コントロール種別で「ラジオボタン」を選択した場合、[項目連携](../../../relating-column-settings/index.md)、[ルックアップ](../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)機能と併用できません。
1. コントロール種別で「ラジオボタン」を選択した場合、[検索機能を使う](table-management-use-search.md)、[複数選択](table-management-multiple-selections.md)、[選択肢にブランクを挿入しない](table-management-not-insert-blank-choice.md)、[アンカー](table-management-anchor.md)の設定は併用できません。
1.  「ラジオボタン」で一度値を選択すると、未選択の状態に戻すことができません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 設定内容

|No|選択肢|説明|
|:----|:----|:----|
|1|ドロップダウンリスト|ドロップダウンリストで値の設定するためのコントロールです。|
|2|ラジオボタン|ラジオボタンで値の設定するためのコントロールです。|

## 動作イメージ

ドロップダウンリスト
![ドロップダウンリストで表示した分類項目](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/e6c535bcdbab4cd58b5b32db369c90d4.png)

ラジオボタン
![ラジオボタンで表示した分類項目](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/c091d7044a314fdf84d008a383807558.png)
フィールドCSSに「radio-clear-both」を設定すると縦に並べることが可能です。
![radio-clear-both を設定し、ラジオボタンを縦に並べた分類項目](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/f3b6792810ac44208574cd8aae270774.png)

## 関連情報

-   [テーブル機能：レコードのエディタ画面](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：項目：分類](../../columns/table-management-class.md)
-   [テーブルの管理：項目：状況](../../columns/table-management-status.md)
-   [テーブルの管理：項目：管理者](../../columns/table-management-manager.md)
-   [テーブルの管理：項目：担当者](../../columns/table-management-owner.md)
-   [テーブルの管理：エディタ：項目連携](../../../relating-column-settings/index.md)
-   [応用編：リンク](../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：エディタ：項目の詳細設定：検索機能を使う](table-management-use-search.md)
-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](table-management-multiple-selections.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢にブランクを挿入しない](table-management-not-insert-blank-choice.md)
-   [テーブルの管理：エディタ：項目の詳細設定：アンカー](table-management-anchor.md)