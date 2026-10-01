---
title: grid.SelectedIds
icon: material/alpha-m-box
category: サーバスクリプト
order: '5000'
status: ''
parts: ''
urlstring: server-script-grid-selected-ids
translationKey: server-script-grid-selected-ids
shortname: grid.SelectedIds
created: 2023-04-10
updated: 2025-01-30
---

## 概要

[サーバスクリプト](../index.md)で一覧画面上の選択しているレコードのIDを取得します。

## 構文

``` javascript
grid.SelectedIds()
```

## パラメータ

なし

## 戻り値

該当するレコードのレコードIDを返却します。

## 使用例

以下の例では選択したレコードのIDをコンソールに表示しています。

##### サンプルコード

```javascript linenums="1"
for (let id of grid.SelectedIds()) {
    context.Log(id);
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.34.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
