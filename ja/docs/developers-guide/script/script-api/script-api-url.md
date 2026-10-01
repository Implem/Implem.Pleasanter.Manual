---
title: $p.apiUrl
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-url
translationKey: script-api-url
shortname: ''
created: 2020-11-02
updated: 2023-08-16
---

## 概要

AjaxのPOSTリクエストによるAPIのリスクエストを実行する際のURL値の取得が可能なメソッドに関する説明をします。

## 構文

##### JavaScript

```
$p.apiUrl(
    <サイトID>,
    <アクションタイプ>
);
``` 

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|サイトID|URLを取得したいサイトID|
|アクションタイプ|get、create、update、delete|

## 使用例

(1) フォルダまたテーブルを作成してください。この例ではサイトIDを109、アクションタイプをgetにしています。
(2) [スクリプト](../../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載し、出力先には[一覧](../../../managers-guide/manage-table/grid/index.md)をチェックして更新します。Wikiの場合、出力先は「編集」をチェックしてください。

##### JavaScript

```
alert('生成されたURLは [' + $p.apiUrl(99999,'get') + '] です。');
``` 

(3) 一覧画面に遷移してください。

##### 結果

```
生成されたURLは [/api/items/99999/get] です。
```