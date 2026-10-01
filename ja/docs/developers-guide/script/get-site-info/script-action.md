---
title: $p.action
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-action
translationKey: script-action
shortname: ''
created: 2020-10-30
updated: 2026-09-07
---

## 概要

AjaxのPOSTリクエストによるアクションの種類が取得できるスクリプト機能になります。

## 構文

##### JavaScript

```
$p.action();
``` 

## 取得可能な値の一覧

|取得可能な画面|取得値|
|:--|:--|
|新規作成画面|new|
|編集画面|edit|
|一覧画面|index|
|カレンダー表示画面|calender|
|クロス集計表示画面|crosstab|
|ガントチャート表示画面|gantt|
|バーンダウンチャート表示画面|burndown|
|時系列チャート表示画面|timeseries|
|カンバン表示画面|kamban|
|画像ライブラリ表示画面|imagelib|
|ゴミ箱画面|trashbox|

## 使用例

(1) フォルダまたテーブルを作成してください(この例ではindexを取得させます)。  
(2) [スクリプト](../../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載し、出力先には[一覧](../../../managers-guide/manage-table/grid/index.md)をチェックして更新します(Wikiの場合は出力先は「編集」をチェック)。  

##### JavaScript

```
alert('この画面のアクションの種類は [' + $p.action() + '] です。');
``` 

(3) 一覧画面に遷移してください。