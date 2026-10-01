---
title: $p.responsive
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-responsive
translationKey: script-responsive
shortname: ''
created: 2021-04-30
updated: 2023-08-16
---

## 概要

レスポンシブスタイルが有効化されているか状態を取得するメソッドです。レスポンシブスタイルの状態によってスクリプトの実行を制御する場合に使用してください。

## 使い方

##### JavaScript

```
$p.responsive()
```    

## サンプルコード

レスポンシブスタイルが有効化されている場合には、インポートボタンとエクスポートボタンを非表示にします。以下のサンプルコードをプリザンターのスクリプトへ設定し出力先は[一覧](../../../managers-guide/manage-table/grid/index.md)にしてください。

##### JavaScript

```
if ($p.responsive()) {
    $('#EditImportSettings').hide();
    $('#OpenExportSelectorDialogCommand').hide();
}
```