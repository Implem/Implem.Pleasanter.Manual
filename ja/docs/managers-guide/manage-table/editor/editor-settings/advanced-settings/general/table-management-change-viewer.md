---
title: ビュワー切替
category: エディタ
order: '3500'
status: ''
parts: ''
urlstring: table-management-change-viewer
translationKey: table-management-change-viewer
shortname: ビュワー切替
created: 2021-01-08
updated: 2026-05-15
---

## 概要

[内容](../../columns/table-management-body.md)と[説明](table-management-column-description.md)のスタイルで[マークダウン](../../../../../../users-guide/common/markdown.md)を選択している項目は、編集画面では「表示」、「編集」の2つの状態に分けれます。 通常は、項目のダブルクリック、または右上の鉛筆アイコンをクリックすることで「編集」モードに。フォーカスが外れると表示モードに、自動で切り替わります。  

## 制限事項

1.  [説明項目](../../columns/table-management-description.md)でのみ使用可能です。
1.  [入力項目のスタイル](table-management-field-css.md)で[マークダウン](../../../../../../users-guide/common/markdown.md)を選択している場合のみ使用可能です。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 設定イメージ

![マークダウンを設定した説明項目の編集画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/eb6e0ffcb64f48e2a9a8b72b74a7751f.png)

ビュワーの切替を変更する場合は[テーブルの管理](../../../../index.md)の[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブで対象の項目を選択し「詳細設定」ボタンをクリックします。  

![エディタタブで項目を選び「詳細設定」ボタンを押す画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/d4fed85b9ae84e8b8428b30992858de9.png)

## 設定種別

![項目の詳細設定の「ビュワー切替」の選択欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/4f5401433ab64b7a86d8f5bf58cbeff8.png)

| 設定 | 説明                                                                                                 |
| :--- | :--------------------------------------------------------------------------------------------------- |
| 自動 | 標準。編集モードで、項目からフォーカスが外れると表示モードに切り替わります。                         |
| 手動 | フォーカスが外れても編集モードを維持します。右上のエンピツをクリックすると表示モードに切り替わります |
| 無効 | 常に編集モードが維持されます                                                                         |

## 編集モード

画像はパスの状態で、マークダウンもレンダリングされず、URLもリンクされた状態にはなりません。

![編集モードの説明項目。マークダウンがそのまま表示される](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/b13dc4cfc79a41b2bf0e64474dadcb27.png)

## 表示モード

画像が表示され、マークダウンがレンダリングされ、URLもリンクされた状態になります。

![表示モードの説明項目。マークダウンがレンダリングされる](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/aeed5b9217d84d8488caa53065e82b5f.png)

## 無効にした場合

「無効」を選択した場合、編集画面では、画像やマークダウンなどは編集モードのままですが、一覧画面では画像表示やマークダウンのレンダリングなどの処理は通常通り行われます。

![ビュワー切替を「無効」にしたときの表示例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/04a0ca4fa9ed4cb693199471ffe3dada.png)

## 関連情報

### 管理者ガイド

-   [テーブルの管理](../../../../index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](table-management-column-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力項目のスタイル](table-management-field-css.md)
-   [テーブルの管理：項目：内容](../../columns/table-management-body.md)
-   [テーブルの管理：項目：説明](../../columns/table-management-description.md)

### ユーザガイド

-   [テーブル機能：レコードのエディタ画面](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [共通機能：マークダウン](../../../../../../users-guide/common/markdown.md)
