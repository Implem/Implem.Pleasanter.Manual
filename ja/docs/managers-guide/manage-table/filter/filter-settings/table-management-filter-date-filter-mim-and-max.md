---
title: 日付項目フィルタの最小、最大、年度、半期、四半期、月
category: フィルタ
order: '600'
status: ''
parts: ''
urlstring: table-management-filter-date-filter-mim-and-max
translationKey: table-management-filter-date-filter-mim-and-max
shortname: 日付項目フィルタの最小、最大、年度、半期、四半期、月
created: 2021-05-10
updated: 2024-07-12
---

## 概要

[日付項目](../../editor/editor-settings/columns/table-management-date.md)の[フィルタ](../../../../users-guide/hands-on/advanced/advanced-operations-link.md)にて[日付フィルタのモード選択](table-management-filter-date-filter-mode.md)で「既定」を選択した際に使用する数値の最小、最大を年単位で指定します。フィルタの選択肢には「今日」、「今月」、「今年」がデフォルトで表示します。

## 制限事項

1. [日付項目](../../editor/editor-settings/columns/table-management-date.md)のみ使用できます。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。
1. 「年度」、「半期」、「四半期」の開始月は[General.json](../../../../setup/parameters/general.json.md)の「FirstMonth」で指定します。既定値は4月です。

## 設定内容

|No|設定項目|説明|
|:----|:----|:----|
|1|最小|-1とした場合、1年前の日付以降の範囲が選択肢に表示されます。年単位の数字を負の整数で入力します。|
|2|最大|1とした場合、1年後の日付までの範囲が選択肢に表示されます。年単位の数字を整数で入力します。|
|3|年度|「チェックボックス」を「オン」にすると「年度」がフィルタの選択肢に表示されます。|
|4|半期|「チェックボックス」を「オン」にすると「半期」がフィルタの選択肢に表示されます。|
|5|四半期|「チェックボックス」を「オン」にすると「四半期」がフィルタの選択肢に表示されます。|
|6|月|「チェックボックス」を「オン」にすると「月」がフィルタの選択肢に表示されます。|

![日付項目フィルタの詳細設定。最小、最大、年度、半期、四半期、月を指定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/filter/assets/657d2dce63424df7bda5cf65f3ba1913.png)

## 関連情報

-   [テーブルの管理：項目：日付](../../editor/editor-settings/columns/table-management-date.md)
-   [応用編：リンク](../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：フィルタ：日付項目フィルタのモード選択](table-management-filter-date-filter-mode.md)
-   [パラメータ設定：General.json](../../../../setup/parameters/general.json.md)