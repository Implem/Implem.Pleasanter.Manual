---
title: スクリプトで読取専用項目の値を取得したい。
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-readonly-value
translationKey: faq-readonly-value
shortname: ''
created: 2020-08-01
updated: 2024-04-29
---

## 回答

「.text()」で取得してください。

---

## 概要

プリザンターでは読取専用項目はspanタグで構成されます（通常はinputタグで構成されます）。[スクリプト](../../managers-guide/manage-table/scripts/index.md)で使用できるjQueryというライブラリの仕様上、inputタグで構成されているものは「.val()」を、spanタグで構成されているものは「.text()」を使用することで値を取得できます。そのため、通常のinputタグを想定しているプリザンターの公式マニュアルやFAQに記載のスクリプトのサンプルコードを使用しても読取専用項目に対しては値を取得できない可能性がありますので、適宜読み替えてください。

### 単位を設定した項目を読取専用にした場合

数値項目で単位を設定した項目を読取専用にした場合、画面上は単位込みの表示となり、「.text()」では単位付きの値を取得します。単位が不要な場合は適宜単位を削除する処理を追加してください。

## サンプルコード

1. 編集画面を開いたタイミングで、読取専用になっているタイトル、分類A、日付Aの値をメッセージに出力するサンプルです。

##### JavaScript

```
$p.events.on_editor_load = function () {
    $p.setMessage(
        '#Message',
        JSON.stringify({
            Css: 'alert-success',
            Text:  `このレコードのタイトルは"${$p.getControl('Title').text()}"、分類Aは"${$p.getControl('ClassA').text()}"、日付Aは"${$p.getControl('DateA').text()}"です。`
        })
    );
}
```

2. 編集画面を開いたタイミングで、読取専用になっている数値A（単位設定あり）の値のみをメッセージに出力するサンプルです。

##### JavaScript

```
$p.events.on_editor_load = function () {
    $p.setMessage(
        '#Message',
        JSON.stringify({
            Css: 'alert-success',
            Text:  `このレコードの数値Aは"${$p.getControl('NumA').text().replace('日','')}"です。`
        })
    );
}
```

## サーバスクリプトを使用する場合

[サーバスクリプト](../../developers-guide/server-script/index.md)を使用する場合は入力可能、読取専用にかかわらず[model](../../developers-guide/server-script/model/index.md)オブジェクトで値を取得できます。読取専用で単位付きの数値項目でも[model](../../developers-guide/server-script/model/index.md)オブジェクトでは値のみ取得します。

## 関連項目

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
-   [開発者ガイド：サーバスクリプト：model](../../developers-guide/server-script/model/index.md)
