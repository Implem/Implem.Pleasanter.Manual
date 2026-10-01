---
title: $NOW関数
category: 計算式
order: '1080'
status: ''
parts: ''
urlstring: formula-function-now
translationKey: formula-function-now
shortname: $NOW関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

現在の日時を取得します。

## 構文

```
$NOW()
```

## パラメータ

なし。

## 戻り値

現在日時（yyyy/mm/dd hh:MM:ss形式）。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。|
|数値（作業量、進捗率、残作業量含む）|表示しない。|
|日付（開始、完了含む ）|戻り値を表示。エディタの書式が「年月日」の場合、表示はしないが登録値には戻り値の時分秒を含む|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

現在の日時が2024/04/01 14:56:43の場合

### 計算式

![$NOW関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/37d09493e9f64ee4be299701bc20ee43.png)

### 計算結果

![$NOW関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c8006a529739495a8216721831d9af04.png)
