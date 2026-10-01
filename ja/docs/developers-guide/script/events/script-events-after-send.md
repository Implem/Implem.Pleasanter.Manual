---
title: $p.events.after_send
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-events-after-send
translationKey: script-events-after-send
shortname: $p.events.after_send,イベント発火スクリプト
created: 2019-08-10
updated: 2024-12-12
---

## 概要

サーバへデータを送信した後に実行するメソッドの指定方法を説明します。

## 制限事項

1.  複数のスクリプトを作成し各スクリプトの内容に本関数を記述すると、スクリプトが上書きされるため、最新のもの以外は動作しません。回避策は以下FAQを参照してください。

    -   [FAQ：$p.events.on_editor_loadを複数設定できるようにしたい](../../../FAQ/features-for-developers/faq-multiple-on-editor-load.md)

## 使い方

``` javascript title="JavaScript" linenums="1"
$p.events.after_send = function (args) {
    // 処理内容
}
```

イベントを発生させるボタンのdata-action属性の値を明示的に記述したい場合は取得してください。

``` javascript title="JavaScript" linenums="1"
$p.events.after_send_{data-action属性の値} = function (args) {
    // 処理内容
}
```

## サンプルコード

1.  「[テーブルの管理](../../../managers-guide/manage-table/index.md)」画面の「[エディタ](../../../managers-guide/manage-table/editor/index.md)」タブを開き、「数値A」項目を追加してください。
1.  テーブルを更新してください。
1.  「テーブルの管理」画面の「[スクリプト](../../../managers-guide/manage-table/scripts/index.md)」タブへ、以下のサンプルコードを設定してください。

    以下のサンプルコードでは、data-action属性の値であるUpdateを明示的に記載してます。

    ``` javascript title="JavaScript" linenums="1"
    $p.events.after_send_Update = function (args) {
        if ($p.getControl('NumA').val() != 100) {
            return false; // falseのときは処理が止まり、更新されない
        } else {
            $p.setMessage('#Message', JSON.stringify(
                {
                    Css: 'alert-success',
                    Text: '数値Aのデータがサーバーに送信されました。'
                }
            ));
            return true; // trueのときは更新される
        }
    }
    ```

1.  「出力先」を「編集」に設定してください。
1.  テーブルを更新してください。
1.  編集画面を開き、数値Aに100を入力して「更新」ボタンを押したときのみ更新されます。

## 関連情報

[FAQ：$p.events.on_editor_loadを複数設定できるようにしたい](../../../FAQ/features-for-developers/faq-multiple-on-editor-load.md)
