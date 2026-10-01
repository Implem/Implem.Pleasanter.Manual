---
title: context.UserData
icon: material/alpha-p-box
category: サーバスクリプト
order: '2000'
status: ''
parts: ''
urlstring: server-script-context-user-data
translationKey: server-script-context-user-data
shortname: context.UserData
created: 2021-10-20
updated: 2026-01-26
---

## 概要

[サーバスクリプト](../index.md)のスクリプト間でデータを共有可能にする機能を提供します。

## プロパティ

`ExpandoObject`のため、任意の名称のプロパティを追加可能。

## メソッド

メソッドはありません。

## 使用例

下記の例では、1つ目のサーバスクリプトでデータベースから取得した情報をユーザデータ MyData に格納し、2つ目のサーバスクリプトでユーザデータ MyData に格納されているデータ件数をログに出力します。条件については1つ目は「更新前」、2つ目「更新後」にチェックしています。

##### JavaScript

``` javascript linenums="1"
// 1つ目のサーバスクリプト
let results = items.Get(10);
context.UserData.MyData = results;
```

##### JavaScript

``` javascript linenums="1"
// 2つ目のサーバスクリプト
let results = context.UserData.MyData;
context.Log(results.Length);
```

## サンプルコード

??? note "1. 一覧画面で平均値との比較で行を色付け"

    一覧画面でテーブル内の任意の数値項目に対し平均値を取得、平均値に対し自身のレコードが低いか高いかで、行に色を付けます。

    また、平均値は画面表示時で1回計算できれば良いため、UserDataに設定し持ち回ることで、余計な計算をさせないように制御します。

    ##### JavaScript

    条件：行表示の前

    ``` javascript linenums="1"
    // UserDataで平均値を持ち回り
    if (!context.UserData.average) {
        context.UserData.average = items.Average(context.SiteId, 'NumA');
    }
    // 行の色付けを平均値と比較して変更
    if (context.UserData.average < model.NumA) {
        model.ExtendedRowCss = 'high';
    } else {
        model.ExtendedRowCss = 'low';
    }
    ```

    ##### CSS
    CSS設定例です。

    ```css linenums="1"
    /* 平均より高い */
    .high td:not(:nth-child(0)) {
        background-color: rgb(235, 175, 175);
    }
    /* 平均より低い */
    .low td:not(:nth-child(0)) {
        background-color: rgb(185, 220, 246);
    }
    ```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.13.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
