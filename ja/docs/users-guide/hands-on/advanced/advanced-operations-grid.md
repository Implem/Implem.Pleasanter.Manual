---
title: ビューモード
category: 操作ガイド（応用編）
order: '20'
status: ''
parts: ''
urlstring: advanced-operations-grid
translationKey: advanced-operations-grid
shortname: 応用編,ビューモード
created: 2023-07-27
updated: 2024-07-01
---

## 概要  

プリザンターではレコードの表示方法として一覧画面の他、様々な形式での表示方法を選択できます。[一覧](../../../managers-guide/manage-table/grid/index.md)の他[カレンダー](../../dashboard/dashboard-calendar.md)、[クロス集計](../../table/record-authoring/data-visualize/table-crostab.md)、[ガントチャート](../../table/record-authoring/data-visualize/table-gantt-chart.md)、[バーンダウンチャート](../../table/record-authoring/data-visualize/table-burndown-chart.md)、[時系列チャート](../../../managers-guide/manage-table/time-series-chart/index.md)、[分析チャート](../../table/record-authoring/data-visualize/table-analy-chart.md)、[カンバン](../../table/record-authoring/data-visualize/table-kanban-chart.md)、「画像ライブラリ」が選択できます。

1.  一覧

    表形式で表示します。表示項目は[テーブルの管理](../../../managers-guide/manage-table/index.md)－[一覧](../../../managers-guide/manage-table/grid/index.md)で設定可能です。

    ![レコードを表形式で表示した一覧画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/6572ad61da7f4f0a8f697da5ed4c9923.png)  

1.  カレンダー

    カレンダー形式で表示します。

    **カレンダータイプ：標準**

    ![カレンダータイプ「標準」でレコードを表示した画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/dfce2bf96e5a47f3ba1890c0f97c26f6.gif)

    **カレンダータイプ：FullCalendar**

    ![カレンダータイプ「FullCalendar」でレコードを表示した画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/72231653dd144bb4b659d8eaac54ab0f.gif)

1.  クロス集計

    指定した項目の件数、合計などのクロス集計を表示します。

    ![指定した項目の件数や合計を集計したクロス集計の画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/27f19f6a0e654d0798d53c089ee86bbb.gif)

1.  ガントチャート

    作業タスクと期間の関係を横棒グラフでチャート表示します。期限付きテーブルのみ選択可能です。

    ![作業タスクと期間を横棒グラフで表したガントチャートの画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/108728c9c43f49019a2f955fc1ebd8ff.gif)

1.  バーンダウンチャート

    作業量と時間の関係を線グラフで表示します。期限付きテーブルのみ選択可能です。

    ![作業量と時間の関係を線グラフで表したバーンダウンチャートの画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/979ef5a35e08443fae324b495e0b2abf.gif)

1.  時系列チャート

    時間経過による値の変化をグラフ表示します。縦軸の値、横軸の日付はそれぞれ任意に選択できます。

    ![値の変化を時間軸で表した時系列チャートの画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/7f840852f409408daf9b4d6ee8d3867a.gif)

1.  分析チャート

    ある時点のデータを円グラフで表示します。記録テーブル・期限付きテーブルで選択可能です。

    ![ある時点のデータを円グラフで表した分析チャートの画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/4acb2a2b14e04f3ebebec495d05eddb8.gif)

1.  カンバン

    主に作業員別のタスクの進捗状況を[カンバン](../../table/record-authoring/data-visualize/table-kanban-chart.md)で表示します。縦軸、横軸の項目はそれぞれ任意に選択できます。表示したレコードをドラッグ＆ドロップすることでレコード内容を更新することができます。

    ![レコードをカードで並べたカンバンの画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/dd93e7702d3b4f7a92b6b00008e54a78.gif)

1.  画像ライブラリ

    内容、説明項目、コメントに貼り付けた画像を一覧で表示します。

    ![貼り付けた画像を並べて表示する画像ライブラリの画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/74dcdc19bcfa4a0bb503c65b174fa31f.png)

### 切り替え方法

ナビゲーションメニューの「表示」メニューからビューモードを切り替えます。

![ビューモードを切り替えるナビゲーションメニューの「表示」メニュー](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/c2d3e8e60b264def8cafddc05d338fc9.png)

### 必要な権限

テーブルの「読取り」権限が必要です。また設定を変更するには「サイトの管理」権限が必要です。

### 利用設定

[一覧](../../../managers-guide/manage-table/grid/index.md)は設定不要です。「読取り権限」があれば表示します。[一覧](../../../managers-guide/manage-table/grid/index.md)以外の表示は[テーブルの管理](../../../managers-guide/manage-table/index.md)より該当のタブを開き、「有効」にチェックしてください。

![テーブルの管理でビューモードの「有効」をチェックする画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/76f004828bd647ecb005fc54d96b2568.png)

## 関連情報

-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [テーブルの管理：一覧画面](../../../managers-guide/manage-table/grid/index.md)
-   [テーブルの管理：時系列チャート](../../../managers-guide/manage-table/time-series-chart/index.md)
-   [テーブル機能：レコードのクロス集計表示](../../table/record-authoring/data-visualize/table-crostab.md)
-   [テーブル機能：レコードのガントチャート表示](../../table/record-authoring/data-visualize/table-gantt-chart.md)
-   [テーブル機能：レコードのバーンダウンチャート表示](../../table/record-authoring/data-visualize/table-burndown-chart.md)
-   [テーブル機能：レコードの分析チャート表示](../../table/record-authoring/data-visualize/table-analy-chart.md)
-   [テーブル機能：レコードのカンバン表示](../../table/record-authoring/data-visualize/table-kanban-chart.md)
-   [ダッシュボード機能：パーツの追加：カレンダー](../../dashboard/dashboard-calendar.md)
