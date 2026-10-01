---
title: $LOGINUSERNAME関数
category: 計算式
order: '0'
status: ''
parts: ''
urlstring: formula-function-loginusername
translationKey: formula-function-loginusername
shortname: ''
created: 2026-08-18
updated: 2026-09-08
---

## 概要

ログイン中のユーザのログインID（表示名となる文字列）を返します。

## 構文

```
$LOGINUSERNAME()
```

## パラメータ

なし。

## 戻り値

現在のログインユーザのユーザID。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。|
|数値（作業量、進捗率、残作業量含む）|表示しない。|
|日付（開始、完了含む ）|表示しない。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

現在のログインユーザのログインIDがHAYATOの場合

### 計算式

![$LOGINUSERNAME関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/e7eb2389fc1f491b85003ad47f9666b8.png)

### 計算結果

![$LOGINUSERNAME関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/55327fad289b47e5af42015a88537b14.png)

