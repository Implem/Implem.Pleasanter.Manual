---
title: context.AddMessage
icon: material/alpha-m-box
category: サーバスクリプト
order: '2000'
status: ''
parts: ''
urlstring: server-script-context-add-message
translationKey: server-script-context-add-message
shortname: context.AddMessage
created: 2021-08-22
updated: 2023-06-21
---

## 概要

[サーバスクリプト](../index.md)でブラウザの下部にメッセージを出力するメソッドです。複数回実行すると複数のメッセージを出力します。

## 構文

``` javascript
context.AddMessage(message, css);
```

## パラメータ

|パラメータ|型|必須|概要|
|:----------|:----------|:---:|:---------------------------|
|message|string|○|メッセージ|
|css|string||CSSクラス名|

## 戻り値

戻り値はありません。

## 使用例

下記の例では、組織ID 3 のユーザが[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)が完了の場合にメッセージを出力します。

##### JavaScript

``` javascript linenums="1"
try {
    if (context.DeptId === 3 && model.Status === 900) {
        context.AddMessage('条件に該当しました。', 'alert-information');
    }
} catch (e) {
    context.Log(e.stack);
}
```

## CSSクラス名

下記のCSSクラス名が使用できます。独自のCSSを作成し割り当てることも可能です。

|CSSクラス名|スタイル|
|:----------|:----------|
|alert-information|青の背景で情報を表します|
|alert-warning|黄色の背景で警告を表します|
|alert-success|緑の背景で警告を表します|
|alert-error|赤の背景でエラーを表します|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：項目：状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
