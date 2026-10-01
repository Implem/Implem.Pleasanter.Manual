---
title: 独自の入力検証を行い、その結果によりメッセージを表示したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-validation-message
translationKey: faq-validation-message
shortname: サンプルコード
created: 2020-11-02
updated: 2024-07-08
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用してください。

---

## 概要

[スクリプト](../../managers-guide/manage-table/scripts/index.md)で独自の入力検証を行う場合はイベント発火スクリプトの[$p.events.before_validate](../../developers-guide/script/events/script-events-before-validate.md)で独自の入力検証と結果メッセージの表示処理を実装してください。

## 操作手順

1.  エディタタブから数値Aの項目を有効化してください。
1.  [スクリプト](../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載し、出力先には「編集」をチェックして更新します。
1.  新規にレコード作成し、編集画面で数値Aに空白や100以外を入力して「更新」ボタンを押します。

### 実行結果

![数値Aが未入力のときに表示される警告メッセージ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/2b731e1d1ce54532a6c09ce6adfde817.png)

![数値Aに100以外を入力したときに表示されるエラーメッセージ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/a0c42c4ceed249d7a89a689e931b99a1.png)

## サンプルコード

``` js title="JavaScript" linenums="1"
$p.events.before_validate_Update = function (args) {
    var myNumA = $p.getControl('NumA').val()
    if (myNumA == "") {
        $p.clearMessage();
        $p.setMessage('#Message', JSON.stringify({
            Css: 'alert-warning',
            Text: '未入力です。数値を入力してください。'
        }));
        return false;   // falseのときは処理が止まり、更新されない
    } else if (myNumA != 100) {
        $p.clearMessage();
        $p.setMessage('#Message', JSON.stringify({
            Css: 'alert-error',
            Text: '数値は100を入力してください。'
        }));
        return false;   // falseのときは処理が止まり、更新されない
    } else {
        return true;    // trueのときは更新される
    }
}
```

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
-   [$p.events.before_validate](../../developers-guide/script/events/script-events-before-validate.md)
