---
title: レコードのクロス集計表示
category: テーブル機能
order: '50'
status: ''
parts: ''
urlstring: table-crostab
translationKey: table-crostab
shortname: クロス集計
created: 2019-04-30
updated: 2026-09-08
---

## 概要

[テーブル](../../index.md)に格納された「レコード」を「クロス集計」形式で表示します。

## 前提条件

* 読取り権限が必要です。

## 操作手順

1. テーブルの一覧画面を開いてください。
1. 「表示」メニューを開き「クロス集計」をクリックしてください。

## 表示の切り替え項目

分類項目を追加するとで縦と横の集計項目を増やすことができます。列の分類では、分類項目もしくは日付項目を選ぶことができます。行の分類では、分類もしくは数値項目を選ぶことができます。集計は、件数、合計、平均、最大、最小を切り替えることができます。日付表示は月、週、日のいずれかを指定することができます。

![列・行の分類や集計方法を切り替えるクロス集計の操作欄](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/40b8ac8be1ae4da8ba4f70946a45e62d.png)

## クロス集計の設定

クロス集計の設定を変更することができます。この操作はサイトの管理権限が必要です。

1. 対象のテーブルを開いてください。
1. 「管理」メニューから[テーブルの管理](../../../../managers-guide/manage-table/index.md)をクリックしてください。
1. 「[クロス集計](../../../../managers-guide/manage-table/crosstab/index.md)」タブを開いてください。
1. 下表に従い設定を行ってください。

    |項目名|説明|設定方法|
    |:---|:---|:---|
    |有効|クロス集計の有効化/無効化を設定|チェックすることでクロス集計を有効化|

1. 画面下部の「更新」ボタンをクリックしてください。

## 列の分類で選択可能な項目の条件

1. 選択肢のある[分類項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)もしくは[日付項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
1. [複数選択](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)の指定がない項目
1. 編集画面で有効化されている項目
1. [項目のアクセス制御](../../../../managers-guide/manage-table/column-access-control/index.md)で読み取り不可になっていない項目

## 行の分類で選択可能な項目の条件

1. 選択肢のある[分類項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)もしくは[数値項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
1. 複数選択以外の項目
1. 編集画面で有効化されている項目
1. [項目のアクセス制御](../../../../managers-guide/manage-table/column-access-control/index.md)で読み取り不可になっていない項目

 ## 0の行を表示しない場合の設定
値のある行のみを表示したい場合、「0の行を表示しない」のチェックをオンにしてください。  

![「0の行を表示しない」のチェック欄](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/fac7f3a18f1e4ed996763185dc6f6385.png)

行で絞り込むことはできますが、列で絞り込むことはできません。

## 関連情報

-   [テーブル機能](../../index.md)
-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)
-   [テーブルの管理：項目：分類](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：日付](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)
-   [項目のアクセス制御](../../../../managers-guide/manage-table/column-access-control/index.md)
-   [テーブルの管理：項目：数値](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)