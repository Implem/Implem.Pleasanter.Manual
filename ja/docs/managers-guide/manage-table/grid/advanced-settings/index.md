---
title: 項目の詳細設定
category: 一覧画面
order: '4'
status: ''
parts: ''
urlstring: table-management-grid-column-settings
translationKey: table-management-grid-column-settings
shortname: 一覧画面の項目の詳細設定
created: 2021-05-06
updated: 2025-11-11
---

## 概要

[一覧画面](../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)の項目の詳細設定では、一覧画面における各項目の表示方法を細かく制御できます。日付項目の[一覧の書式](table-management-grid-format.md)を除き、設定項目は共通です。

#### 日付項目の詳細設定画面

![日付項目の一覧画面の詳細設定ダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/06beb1cc5db44bab8b6626a544262820.png)

#### それ以外の項目の詳細設定画面

![日付以外の項目の一覧画面の詳細設定ダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/3c5913304cb4477996e82c49e72a6350.png)

## 制限事項

1. 他のテーブルの項目の詳細設定は行えません。対象のテーブルに移動して設定する必要があります。
1. [セルの横幅](table-management-grid-cell-width.md)はバージョン1.4.20.0以降で利用できます。
1. [左端でスクロール固定](table-management-grid-sticky-on-left-edge.md)はバージョン1.4.20.0以降で利用できます。
1. [セル幅で文字を折り返す](table-management-grid-wordwrap.md)はバージョン1.4.22.0以降で利用できます。

## 前提条件

設定を行うには「サイトの管理権限」が必要です。

## 操作手順

1. 対象のテーブルを開いてください。
1. 「管理」メニューからテーブルの管理をクリックしてください。
1. 一覧タブを開いてください。
1. 「現在の設定」のリストから対象の項目を1つ選択し「詳細設定」ボタンをクリックしてください。
1. 「入力項目」の「詳細設定」を行うダイアログが表示されるので、必要な設定を行い「変更」ボタンをクリックしてください。
1. 画面下部の「更新」ボタンをクリックしてください。

## 詳細設定の設定項目

以下の設定項目があります。

|設定項目|内容|
|---|---|
|[表示名](../../editor/editor-settings/advanced-settings/general/table-management-label-text.md)|一覧画面上の項目のヘッダに表示する文字列を指定する|
|[一覧の書式](table-management-grid-format.md)|一覧画面上の日付項目の表示形式を設定する（日付項目のみ）|
|[セルCSS](../../../../FAQ/grid/faq-grid-cell-color-by-num-range.md)|一覧画面上の項目のth要素、td要素に出力するCSSクラス名を設定する|
|[左端でスクロール固定](table-management-grid-sticky-on-left-edge.md)|特定の項目（列）を表示させたまま、一覧画面の検索結果一覧と一覧編集をスクロールする|
|[セルの横幅](table-management-grid-cell-width.md)|一覧画面の項目の横幅をピクセル単位で指定する|
|[セル幅で文字を折り返す](table-management-grid-wordwrap.md)|オンにすると項目の内容をセル幅で折り返し表示する|
|[カスタムデザインを使用](table-management-use-grid-design.md)|一覧画面上の「セル」に複数の項目を表示する|

[一覧の書式](table-management-grid-format.md)の選択肢と表示形式は次の通りです。日付の表示形式は、ユーザの[言語](../../../../FAQ/system-requirements-and-setup/faq-supported-language.md)設定に応じて変わります。

|選択肢|ユーザの言語設定が日本語の場合の表示形式|
|---|---|
|月日|`MM/dd`|
|年月|`yyyy/MM`|
|年月日|`yyyy/MM/dd`|
|年月曜日|`yyyy/MM/dd ddd`|
|日付と曜日と時刻(分)|`yyyy/MM/dd ddd HH:mm`|
|日付と曜日と時刻(秒)|`yyyy/MM/dd ddd HH:mm:ss`|
|日付と時刻(分)|`yyyy/MM/dd HH:mm`|
|日付と時刻(秒)|`yyyy/MM/dd HH:mm:ss`|

## 対応バージョン

|対応バージョン|内容|
|---|---|
|バージョン1.4.20.0以降|セルの横幅、左端でスクロール固定を追加|
|バージョン1.4.22.0以降|セル幅で文字を折り返すを追加|

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：一覧の書式](table-management-grid-format.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：セルの横幅](table-management-grid-cell-width.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：左端でスクロール固定](table-management-grid-sticky-on-left-edge.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：セル幅で文字を折り返す](table-management-grid-wordwrap.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../../editor/editor-settings/advanced-settings/general/table-management-label-text.md)
-   [FAQ：一覧画面で数値の範囲によってセルの色を変えたい](../../../../FAQ/grid/faq-grid-cell-color-by-num-range.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：カスタムデザインを使用](table-management-use-grid-design.md)
-   [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../../FAQ/system-requirements-and-setup/faq-supported-language.md)