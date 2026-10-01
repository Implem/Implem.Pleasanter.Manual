---
title: $p.events.before_set
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-events-before-set
translationKey: script-events-before-set
shortname: $p.events.before_set,イベント発火スクリプト
created: 2019-08-10
updated: 2024-12-12
---

## 概要

サーバへデータを送信後、画面内容を更新する前に実行するメソッドの指定方法を説明します。

## 制限事項

1. 複数のスクリプトを作成し各スクリプトの内容に本関数を記述すると、スクリプトが上書きされるため、最新のもの以外は動作しません。回避策は以下FAQを参照してください。

    -   [FAQ：$p.events.on_editor_loadを複数設定できるようにしたい](../../../FAQ/features-for-developers/faq-multiple-on-editor-load.md)

## 使い方

##### JavaScript

```
$p.events.before_set = function (args) {
    //処理内容
}
または
$p.events.before_set_{data-action属性の値} = function (args) {
    //処理内容
}
```    
※イベントを発生させるボタンのdata-action属性の値を明示的に記述したい場合は取得してください。

## サンプルコード

以下のサンプルコードをプリザンターのスクリプトへ設定し出力先は「編集」にした後、「更新」ボタンを押下します(当例ではdata-action属性の値であるUpdateを明示的に記載してます)。

##### JavaScript

```
$p.events.before_set_Update = function () {
    $p.setMessage('#Message', JSON.stringify({
        Css: 'alert-success',
        Text: '画面更新前です。'
        })
    );
}
```

## 関連情報

[FAQ：$p.events.on_editor_loadを複数設定できるようにしたい](../../../FAQ/features-for-developers/faq-multiple-on-editor-load.md)