---
title: $p.events.on_calendar_load
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-events-on-calendar-load
translationKey: script-events-on-calendar-load
shortname: $p.events.on_calendar_load
created: 2022-05-06
updated: 2025-05-28
---

## 概要

[カレンダー](../../../users-guide/dashboard/dashboard-calendar.md)を読み込んだとき、もしくはフィルタ等で表示する内容が変わったときに実行するメソッドの指定方法を説明します。

## 制限事項

1. 意図しないタイミングで処理が実行されてしまう等の影響がある場合を除き、出力先は「全て」を選択してください。
1. 複数のスクリプトを作成し各スクリプトの内容に本関数を記述すると、スクリプトが上書きされるため、最新のもの以外は動作しません。回避策は以下FAQを参照してください。

    -   [FAQ：$p.events.on_editor_loadを複数設定できるようにしたい](../../../FAQ/features-for-developers/faq-multiple-on-editor-load.md)

## 構文

##### JavaScript

```
$p.events.on_calendar_load = function () {
    //処理内容
}
```    

## 使用例

以下のサンプルコードをプリザンターのスクリプトへ設定すると、カレンダー画面を読み込んだときに画面下部にメッセージを表示します。

##### JavaScript

```
$p.events.on_calendar_load = function () {
    $p.setMessage('#Message', JSON.stringify({
        Css: 'alert-success',
        Text: 'カレンダー画面を読み込みました。'
        })
    );
}
```

## 関連情報

-   [ダッシュボード機能：パーツの追加：カレンダー](../../../users-guide/dashboard/dashboard-calendar.md)
-   [FAQ：$p.events.on_editor_loadを複数設定できるようにしたい](../../../FAQ/features-for-developers/faq-multiple-on-editor-load.md)