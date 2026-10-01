---
title: $p.events.before_send
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-events-before-send
translationKey: script-events-before-send
shortname: $p.events.before_send,イベント発火スクリプト
created: 2019-08-10
updated: 2024-12-12
---

## 概要

サーバへデータを送信する前に実行するメソッドの指定方法を説明します。項目に入力した値が正しいかをチェックするときに使用してください。

## 制限事項

1. 複数のスクリプトを作成し各スクリプトの内容に本関数を記述すると、スクリプトが上書きされるため、最新のもの以外は動作しません。回避策は以下FAQを参照してください。

    -   [FAQ：$p.events.on_editor_loadを複数設定できるようにしたい](../../../FAQ/features-for-developers/faq-multiple-on-editor-load.md)

## 構文

##### JavaScript

```
$p.events.before_send = function (args) {
    //処理内容
}
または
$p.events.before_send_{data-action属性の値} = function (args) {
    //処理内容
}
```    
※イベントを発生させるボタンのdata-action属性の値を明示的に記述したい場合は取得してください。

## 使用例

以下のサンプルコードをプリザンターのスクリプトへ設定し出力先は「編集」にした後、編集画面で数値Aに100を入力して「更新」ボタンを押下してください。  
正しく入力された時のみ分類Aに値がセットされ、画面が更新されます(当例ではdata-action属性の値であるUpdateを明示的に記載してます)。

##### JavaScript

```
$p.events.before_send_Update = function (args) {
    if ($p.getControl('NumA').val() != 100) {
        return false; //falseのときは処理が止まり、更新されない
    } else {
        $p.set($p.getControl('ClassA'), '正しく入力されました。')
        return true;  //trueのときは更新される
    }
}
```

## 関連情報

[FAQ：$p.events.on_editor_loadを複数設定できるようにしたい](../../../FAQ/features-for-developers/faq-multiple-on-editor-load.md)