---
title: レコードの分析チャート表示
category: テーブル機能
order: '10'
status: ''
parts: ''
urlstring: table-analy-chart
translationKey: table-analy-chart
shortname: 分析チャート
created: 2023-10-24
updated: 2026-01-13
---

## 概要

テーブルに格納されたレコードを分析チャート形式で表示します。

## 前提条件

サイトの読取権限が必要です。

## 操作手順

1. テーブルの一覧画面を開いてください。
2. ナビゲーションメニューより「表示」－「分析チャート」をクリックしてください。
3. 追加ボタンをクリックしてください。
![分析チャート画面の「追加」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/f24d57649d8f4ecb91f7423bd253cb61.png)

4. 分析パーツのダイアログ画面にて、作成条件を指定してください。
![作成条件を指定する分析パーツのダイアログ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/425681d09d794ea69c124a2cccd97afd.png)

### 分析パーツ（作成条件）

| No | 項目| 説明 |
|:---|:---|:---|
| 1 | 項目 | 円グラフでグループに分ける項目を[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)、「管理者」、「担当者」、「分類A（有効化した選択肢ありの分類項目）等」、「作成者」、「更新者」から指定します。 |
| 2 | 値（左：数値） | 集計時点とする数値を指定します。 |
| 3 | 値（右：期間） | 集計時点とする期間を「日前」、「ヶ月前」、「年前」、「時間前」、「分前」、「秒前」から選択します。 |
| 4 | 集計種別 | どのように集計するかを「件数」、「合計」、「平均」、「最大」、「最小」から選択します。 |
| 5 | 集計対象 | 何を集計するかを「作業量」、「残作業量」、「数値A（有効化した数値項目）等」から選択します。 |

5. 追加ボタンをクリックします。
![分析パーツのダイアログの「追加」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/60dde030552b422fbc87463ff2098168.png)

6. 円グラフが追加されます。
![追加された円グラフが表示された分析チャート画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/9557ac3e8baa4bc3826ba7be7f793c2b.png)

7. 円グラフを削除したい場合はマウスをホバーして表示される×ボタンをクリックします。
![円グラフにマウスをホバーすると表示される×ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/5c5f623c3cce41ec98f2f8bf1d156107.png)

8. 複数の円グラフを表示することも可能です。同名のラベルは比較ができるように同じ色で表示されます。
![複数の円グラフを並べて表示した分析チャート画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/bfb3204cdf0541779b625e934ba7dcf6.png)

9. 該当するデータが存在しない場合は、エラーメッセージが表示されます。
![該当するデータがない場合に表示されるエラーメッセージ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/f59e95892c984f74bb772e44bf0b9e31.png)

## 使用例

以下のようなレコードがあった場合（数値Aを有効化）
![使用例で用いる、数値Aを持つレコードの一覧](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/a18200299f8246898f052d2799912d96.png)

#### 状況ごとの件数を集計したい場合

1. 分析パーツのダイアログ画面で項目に[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)、集計種別に「件数」を指定します。

2. 以下のようにグラフが表示されます。
![状況ごとの件数を集計した円グラフ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/83ae95b2a78c4a3cb5195943458f7420.png)

#### 状況ごとの数値Aの合計を集計したい場合

1. 分析パーツのダイアログ画面で項目に[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)、集計種別に「合計」、集計対象に「数値A」を指定します。

2. 以下のようにグラフが表示されます。
![状況ごとの数値Aの合計を集計した円グラフ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/6100491c116c4e6c840f3521dd1570f1.png)

## 分析チャートの円グラフの表示色について

分析チャートの円グラフの表示色は、JavaScriptのライブラリ「D3.js」で使用できるカラーセットを利用しています。チャートの識別がしやすいよう、表示数によって使用するカラーセットが異なります。

|表示数|カラーセット|d3-scale名称|
|:---|:---|:---|
|10個以下|10色のカラーセット|d3.schemeCategory10|
|11個以上|20色のカラーセット|d3.interpolateRainbow|

20色のカラーセットでは以下のようなイメージで表示されます。
![20色のカラーセットで表示した円グラフの例](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/f7ae440c3b4f447badd5bd603ed7875e.png)

### 参考URL

https://github.com/d3/d3-scale-chromatic/blob/main/README.md

## 分析チャートの設定

分析チャートの設定を変更することができます。この操作はサイトの管理権限が必要です。

1. 対象のテーブルを開いてください。
2. 「管理」メニューから[テーブルの管理](../../../../managers-guide/manage-table/index.md)をクリックしてください。
3. 「[分析チャート](../../../../managers-guide/manage-table/analysis-chart/index.md)」タブを開いてください。
4. 下表に従い設定を行ってください。

|項目名|説明|設定方法|
|:---|:---|:---|
|有効|分析チャートの有効化/無効化を設定|チェックすることで分析チャートを有効化|

5. 画面下部の「更新」ボタンをクリックしてください。

## 関連情報

-   [テーブルの管理：項目：状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)