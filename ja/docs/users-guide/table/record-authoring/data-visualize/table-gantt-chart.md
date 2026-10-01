---
title: レコードのガントチャート表示
category: テーブル機能
order: '60'
status: ''
parts: ''
urlstring: table-gantt-chart
translationKey: table-gantt-chart
shortname: ガントチャート
created: 2019-04-30
updated: 2024-06-07
---

## 概要

[テーブル](../../index.md)に格納された「レコード」を「ガントチャート」形式で表示します。

## 前提条件

* 読取り権限が必要です。
* 期限付きテーブルで選択可能です。記録テーブルでは「表示」メニューに「ガントチャート」は表示しません。

## 操作手順

1. テーブルの一覧画面を開いてください。
1. 「表示」メニューを開き「ガントチャート」をクリックしてください。

## 表示の切り替え項目

[分類](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)を指定すると状況や担当者ごとにグループ化して表示できます。[ソート](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)を指定すると指定した項目で昇順に並び替えることができます。「開始日」を指定するとでチャートの開始位置を変更することができます。「前」もしくは「次」ボタンをクリックすると7日分だけ前後に移動します。「初日」ボタンをクリックするとサイト内で「開始」が最も早く設定されているレコードを基準にして表示します。「今日」ボタンをクリックすると開始日を今日として表示します。「期間」スライダーを調整することで、チャートに表示する日数を7日から、登録されたレコードの最も先の完了日を上限とした期間で変更することができます。

## チャートの表示について

* ブルー：完了
* グリーン：予定より前倒し
* ピンク：予定より遅延

## レコードの操作

1. レコードをクリックするとエディタ画面に遷移します。

![レコードが横棒で並ぶガントチャートの画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-visualize/assets/cae2dac0ac3a447f8b45acaabd24d4da.png)

## ガントチャートの設定

ガントチャートの設定を変更することができます。この操作はサイトの管理権限が必要です。

1. 対象のテーブルを開いてください。
1. 「管理」メニューから[テーブルの管理](../../../../managers-guide/manage-table/index.md)をクリックしてください。
1. 「[ガントチャート](../../../../managers-guide/manage-table/gantt-chart/index.md)」タブを開いてください。
1. 下表に従い設定を行ってください。

    |項目名|説明|設定方法|
    |:---|:---|:---|
    |有効|ガントチャートの有効化/無効化を設定|チェックすることでガントチャートを有効化|
    |進捗率を表示|各レコードの進捗率の表示を有効化/無効化する設定|チェックすることで進捗率の表示を有効化|

1. 画面下部の「更新」ボタンをクリックしてください。

## 関連情報

-   [テーブル機能](../../index.md)
-   [テーブルの管理：項目：分類](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)
-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)