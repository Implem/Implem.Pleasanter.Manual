---
title: 一覧の書式
category: 一覧画面
order: '20'
status: ''
parts: ''
urlstring: table-management-grid-format
translationKey: table-management-grid-format
shortname: 一覧の書式
created: 2021-05-06
updated: 2025-10-24
---

## 概要

[一覧画面](../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)上の[日付項目](../../editor/editor-settings/columns/table-management-date.md)の表示フォーマットを設定します。  

## 制限事項

1. [作成日時項目](../../editor/editor-settings/columns/table-management-created-time.md)、[更新日時項目](../../editor/editor-settings/columns/table-management-updated-time.md)、[日付項目](../../editor/editor-settings/columns/table-management-date.md)でのみ使用可能です。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 操作方法

1. [一覧画面の項目の詳細設定](index.md)を参照してください。

## 設定内容

App_Data\Displaysフォルダ配下のjsonファイルの書式で表示されます。

|No|選択肢|説明|
|:----|:----|:----|
|1|月日|MdFormat.jsonの形式で表示(例：`MM/dd`)|
|2|年月|YmFormat.jsonの形式で表示(例：`yyyy/MM`)|
|3|年月日|YmdFormat.json の形式で表示(例：`yyyy/MM/dd`)|
|4|年月曜日|YmdaFormat.json の形式で表示(例：`yyyy/MM/dd ddd`)|
|5|日付と曜日と時刻(分)|YmdahmFormat.json の形式で表示(例：`yyyy/MM/dd ddd HH:mm`)|
|6|日付と曜日と時刻(秒)|YmdahmsFormat.json の形式で表示(例：`yyyy/MM/dd ddd HH:mm:ss`)|
|7|日付と時刻(分)|YmdhmFormat.json の形式で表示(例：`yyyy/MM/dd HH:mm`)|
|8|日付と時刻(秒)|YmdhmsFormat.json の形式で表示(例：`yyyy/MM/dd HH:mm:ss`)|

※ユーザの言語設定に対応するフォーマットが表示されます。

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理：項目：日付](../../editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：作成日時](../../editor/editor-settings/columns/table-management-created-time.md)
-   [テーブルの管理：項目：更新日時](../../editor/editor-settings/columns/table-management-updated-time.md)
-   [テーブルの管理：一覧画面：項目の詳細設定](index.md)