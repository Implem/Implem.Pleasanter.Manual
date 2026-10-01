---
title: $p.events.on_grid_load
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-events-on-grid-load
translationKey: script-events-on-grid-load
shortname: $p.events.on_grid_load,イベント発火スクリプト
created: 2019-08-10
updated: 2025-05-28
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)または[ダッシュボード](../../../users-guide/dashboard/dashboard-add-parts.md)を読み込んだとき、もしくはフィルタ等で表示する内容が変わったときに実行するメソッドの指定方法を説明します。

## 制限事項

1. 意図しないタイミングで処理が実行されてしまう等の影響がある場合を除き、出力先は「全て」を選択してください。
1. 複数のスクリプトを作成し各スクリプトの内容に本関数を記述すると、スクリプトが上書きされるため、最新のもの以外は動作しません。回避策は以下FAQを参照してください。

    -   [FAQ：$p.events.on_editor_loadを複数設定できるようにしたい](../../../FAQ/features-for-developers/faq-multiple-on-editor-load.md)

## 構文

##### JavaScript

```
$p.events.on_grid_load = function () {
    //処理内容
}
```    

## 使用例

以下のサンプルコードをプリザンターのスクリプトへ設定すると、一覧画面を読み込んだときに画面下部にメッセージが表示されます。

##### JavaScript

```
$p.events.on_grid_load = function () {
    $p.setMessage('#Message', JSON.stringify({
        Css: 'alert-success',
        Text: '一覧画面を読み込んだので、画面を表示します。'
    }));
}
```

## 関連情報

[FAQ：$p.events.on_editor_loadを複数設定できるようにしたい](../../../FAQ/features-for-developers/faq-multiple-on-editor-load.md)