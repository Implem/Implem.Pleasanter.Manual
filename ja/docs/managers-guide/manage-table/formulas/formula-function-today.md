---
title: $TODAY関数
category: 計算式
order: '1100'
status: ''
parts: ''
urlstring: formula-function-today
translationKey: formula-function-today
shortname: $TODAY関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

現在の日付を取得します。

## 構文

```
$TODAY()
```

## パラメータ

なし。

## 戻り値

現在日付（yyyy/mm/dd形式）。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。|
|数値（作業量、進捗率、残作業量含む）|表示しない。|
|日付（開始、完了含む ）|戻り値を表示。エディタの書式が「日付と時刻（分）」、「日付と時刻（秒）」の場合は00:00:00を自動補完。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

現在の日付が2024/04/01の場合

### 計算式

![$TODAY関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/95480abd6f81407c908ac94df558d3bf.png)

### 計算結果

![$TODAY関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/12da2c6d499d48c9ba11f2122439e85d.png)
