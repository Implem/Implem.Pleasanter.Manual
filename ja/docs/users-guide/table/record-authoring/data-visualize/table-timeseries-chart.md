---
title: レコードの時系列チャート表示
category: テーブル機能
order: '80'
status: ''
parts: ''
urlstring: table-timeseries-chart
translationKey: table-timeseries-chart
shortname: 時系列チャート
created: 2019-04-30
updated: 2024-06-07
---

## 概要

[テーブル](../../index.md)に格納された「レコード」を[時系列チャート](../../../../managers-guide/manage-table/time-series-chart/index.md)形式で表示します。

## 前提条件

* 読取り権限が必要です。

## 操作手順

1. テーブルの一覧画面を開いてください。
1. 「表示」メニューを開き[時系列チャート](../../../../managers-guide/manage-table/time-series-chart/index.md)をクリックしてください。

## 表示の切り替え項目

[時系列チャート](../../../../managers-guide/manage-table/time-series-chart/index.md)では、「面」と「折れ線」の2種類からチャートを選択できます。
面チャートと折れ線チャートの切り替えについての画面イメージは次のとおりです。

### 面チャート

![面チャートで表示した時系列チャート](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/9c9c586bb9eb4b53b9dfe5c889b3206f.png)

### 折れ線チャート

![折れ線チャートで表示した時系列チャート](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/f6b3838ae95e47f6b05c1bda87e88609.png)

縦軸および横軸は、チャート上部の各項目を選択することで切り替えが行えます。

| No | 項目| 説明 |
|:---|:---|:---|
| 1 | 分類 | 縦軸を分類項目から選択します。 |
| 2 | 集計種別 | 「件数」、「合計」、「平均」、「最大」、「最小」から選択します。 |
| 3 | 集計対象(※1) | 任意の数値項目または「作業量」、「残作業量」から選択します。 |
| 4 | チャートの種類 |「面」または「折れ線」から選択します。 |
| 5 | 横軸 | 任意の日付項目または[履歴](../../../../managers-guide/manage-table/history/index.md)、「開始」、「完了」から選択します。|

※1 「集計対象」項目は、「集計種別」の「件数」以外を選択した場合のみ画面に表示されます。

## チャート表示の内容について

「チャートの種類」の選択、「横軸」項目の選択によってチャート表示の内容が異なります。

### 面チャート

|横軸|チャート表示|
|:---|:---|
|履歴|各分類の要素を上に積み上げたチャート|
|履歴以外|各分類の要素を個別に集計したチャート|

### 折れ線チャート

|横軸|チャート表示|
|:---|:---|
|全ての項目|各分類の要素を個別に集計したチャート|

## 折れ線チャートの表示色について

折れ線チャートの表示色は、JavaScriptのライブラリ「D3.js」で使用できるカラーセットを利用しています。チャートの識別がしやすいよう、表示数によって使用するカラーセットが異なります。

|表示数|カラーセット|d3-scale名称|
|:---|:---|:---|
|10個以下|10色のカラーセット|d3.schemeCategory10|
|11個以上|20色のカラーセット|d3.interpolateRainbow|

### 参考URL

https://github.com/d3/d3-scale-chromatic/blob/main/README.md

## 時系列チャートの設定

[時系列チャート](../../../../managers-guide/manage-table/time-series-chart/index.md)の設定を変更することができます。この操作はサイトの管理権限が必要です。

1. 対象のテーブルを開いてください。
1. 「管理」メニューから[テーブルの管理](../../../../managers-guide/manage-table/index.md)をクリックしてください。
1. [時系列チャート](../../../../managers-guide/manage-table/time-series-chart/index.md)タブを開いてください。
1. 下表に従い設定を行ってください。

|項目名|説明|設定方法|
|:---|:---|:---|
|有効|時系列チャートの有効化/無効化を設定|チェックすることで時系列チャートを有効化|

5. 画面下部の「更新」ボタンをクリックしてください。

## 関連情報

-   [テーブル機能](../../index.md)
-   [テーブルの管理：時系列チャート](../../../../managers-guide/manage-table/time-series-chart/index.md)
-   [テーブルの管理：履歴](../../../../managers-guide/manage-table/history/index.md)
-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)