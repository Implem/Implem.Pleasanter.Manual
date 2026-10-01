---
title: 一覧の設定
category: 一覧画面
order: '3'
status: ''
parts: ''
urlstring: table-management-grid-columns
translationKey: table-management-grid-columns
shortname: 一覧画面の項目の設定
created: 2021-05-06
updated: 2025-09-19
---

## 概要

[一覧](index.md)の項目の「有効化」、「無効化」を設定することができます。[リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)を使用すると「マスタテーブル」など関連する他の[テーブル](../../../users-guide/table/index.md)の[項目](../editor/editor-settings/columns/index.md)を表示することが可能です。[一覧画面の項目の詳細設定](advanced-settings/index.md)では更に詳細な設定を行うことができます。

## 制限事項

1. [リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)を設定した[分類項目](../editor/editor-settings/columns/table-management-class.md)の[複数選択](../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)を「有効化」している場合には、他の[テーブル](../../../users-guide/table/index.md)の[項目](../editor/editor-settings/columns/index.md)を表示することができません。
1. [項目](../editor/editor-settings/columns/index.md)を「無効化」しても[一覧画面の項目の詳細設定](advanced-settings/index.md)で行った変更は保持されます。再度「有効化」した際に変更された状態で戻ります。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。
1. 他のテーブルの項目を表示するには事前に[リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)の設定が必要です。

## 操作手順

1. 対象の[テーブル](../../../users-guide/table/index.md)を開いてください。
1. 「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1. [一覧](index.md)タブを開いてください。
1. [選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)のリストから対象の[項目](../editor/editor-settings/columns/index.md)を選択してください。他のテーブルから選択する場合には[選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)から対象の[テーブル](../../../users-guide/table/index.md)を選択すると[選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)の内容が変化します。
1. 「有効化」ボタンをクリックしてください。
1. 「有効化」した[項目](../editor/editor-settings/columns/index.md)が「現在の設定」の一番下に追加されるので「上」、「下」ボタンを使用して、表示する位置を調整してください。Ctrlキーを押しながら「上」、「下」ボタンをクリックすると[項目](../editor/editor-settings/columns/index.md)が最上段、最下段に移動します。
1. 不要な[項目](../editor/editor-settings/columns/index.md)は「現在の設定」から選択して「無効化」ボタンをクリックしてください。
1. 画面下部の「更新」ボタンをクリックしてください。

### 一覧画面の「 サイト 」を有効化した際に表示される内容

一覧画面の「 サイト 」列に、データが登録されているテーブルの名称が表示されます。サイト統合を行わずにテーブルを使用している場合はすべての行に同じテーブルの名称が表示されますが、サイト統合している場合は2種類以上のテーブルの名称が表示される可能性があります。サイト統合の手順については、[サイト統合](../../../users-guide/table/record-authoring/edit-records/table-site-integration.md)のマニュアルを参照してください。

## 動作イメージ

下図の例では「商談」テーブルの[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)に表示する項目を「有効化」しています。リンクしている「顧客」テーブルから「住所」と「連絡先」を選択し、表示しています。
![「商談」テーブルの一覧の設定。リンク先の「顧客」から住所と連絡先を有効化](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/ee679c472e39446ea0f7cf4bb53962f9.png)

## 関連情報

-   [テーブルの管理：一覧画面](index.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [テーブルの管理：項目](../editor/editor-settings/columns/index.md)
-   [テーブルの管理：一覧画面：項目の詳細設定](advanced-settings/index.md)
-   [テーブルの管理：項目：分類](../editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [テーブル機能：サイト統合](../../../users-guide/table/record-authoring/edit-records/table-site-integration.md)
-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)