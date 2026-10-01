---
title: ページ当たりの表示件数
category: 一覧画面
order: '240'
status: ''
parts: ''
urlstring: table-management-grid-page-size
translationKey: table-management-grid-page-size
shortname: ページ当たりの表示件数
created: 2021-05-06
updated: 2023-05-12
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)では「ページ当たりの表示件数」に指定した件数の「レコード」を取得して一覧表示を行います。スクロールを行うと、同様に「ページ当たりの表示件数」に指定した件数の「レコード」を取得し一覧表示の下部に「レコード」を追加表示します。これにより大量のデータが格納されている[テーブル](../../../users-guide/table/index.md)においても全件取得することなく「レコード」の「一覧表示」が行えます。既定値は20件です。「ページ当たりの表示件数」の下限、上限を変更する場合には[General.json](../../../setup/parameters/general.json.md)の「GridPageSizeMin」および「GridPageSizeMax」を変更してください。

## 注意事項

1. 「ページ当たりの表示件数」が多すぎる場合、データの取得や画面表示に時間がかかりパフォーマンスが悪化する可能性があります。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [パラメータ設定：General.json](../../../setup/parameters/general.json.md)