---
title: context.QueryStrings
icon: material/alpha-p-box
category: サーバスクリプト
order: '2000'
status: ''
parts: ''
urlstring: server-script-context-query-strings
translationKey: server-script-context-query-strings
shortname: context.QueryStrings
created: 2022-07-19
updated: 2026-01-26
---

## 概要

[サーバスクリプト](../index.md)でURL文字列に含まれるQueryパラメータの値を取得します。

## メソッド

|No|Name|Description|
|:----|:----|:----|
|1|Data|パラメータ値を文字列型で取得します|
|2|Bool|パラメータ値を真偽値型で取得します|
|3|Int|パラメータ値を整数型で取得します|

## 使用例

下記の例では、`http://example.com/items/1000/index?name=Hayato&id=123` でアクセスされた際のURL文字列に含まれるパラメータ（`name`、`id`）の値を取得します。

##### JavaScript

``` javascript linenums="1"
let name = context.QueryStrings.Data('name'); 
context.Log(name);    // Hayato

let id = context.QueryStrings.Int('id');
context.Log(id);    // 123
```

## サンプルコード

??? note "1. 外部から一覧にアクセス時に任意のステータスでフィルタする"

    以下のようなURLで一覧画面に遷移したとき、状況が完了（900）でフィルタした状態で画面を表示します。

    ``` text
    /items/XXXXXX/index?status=900
    ```

    たとえば、外部システムからURLでリンクする際、リンク文字列生成時にパラメータを付与することで、フィルタした状態の一覧画面へ遷移が可能となります。

    ##### JavaScript

    条件：ビュー処理時

    ``` javascript linenums="1"
    let statusParam = context.QueryStrings.Data('status');
    if (statusParam) {
        view.Filters.Status = `["${statusParam}"]`;
    }
    ```

??? note "2. 参照コピー時、コピー元のレコードIDを取得する"

    参照コピー時に、コピー元のレコードIDを取得し任意の項目へ設定します。

    参照コピー時には以下のようなURLで新規作成画面へ遷移します。

    ``` text
    /items/9999/new?CopyFrom=8888
    ```

    このCopyFromがコピー元のレコードIDとなるため、QueryStringsで取得します。

    ##### JavaScript

    条件：画面表示の前

    ``` javascript linenums="1"
    if (context.Action === 'new') {
        const copyFromId = context.QueryStrings.Data('CopyFrom');
        if (copyFromId) model.ClassA = copyFromId;
    }
    ```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.15.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
