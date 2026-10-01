---
title: $p.setMessage
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-set-message
translationKey: script-set-message
shortname: ''
created: 2019-08-14
updated: 2023-07-20
---

## 概要

任意のメッセージや、エラーを表示したいとき画面下部に任意のメッセージを表示させるメソッドの説明になります。

## 構文

##### JavaScript

```
$p.setMessage('#Message', JSON.stringify({
    Css: <メッセージタイプ>,
    Text: <任意のメッセージ>
}));
```

## メッセージタイプ

|種類|説明|
|:--|:--|
|alert-success|正常を表す、緑色のメッセージ欄|
|alert-warning|注意を表す、黄色のメッセージ欄|
|alert-error|異常を表す、赤色のメッセージ欄| 

## 使用例

##### JavaScript

```
$p.setMessage('#Message', JSON.stringify({
    Css: 'alert-success',
    Text: '処理が正常に終了しました。'
}));
```