---
title: $POWER関数
category: 計算式
order: '1375'
status: ''
parts: ''
urlstring: formula-function-power
translationKey: formula-function-power
shortname: $POWER関数
created: 2023-12-27
updated: 2024-06-07
---

## 概要

数値のべき乗を返します。

## 構文

```
$POWER(数値, 指数)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|数値|半角数値|必須|べき乗の底|
|指数|半角数値|必須|数値を底とするべき乗の指数|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|数値|〇|〇|×|〇|×|
|指数|〇|〇|×|〇|×|

## 戻り値

数値を除数で割ったときの剰余。 戻り値は除数と同じ符号。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。値付きドロップダウンリストの場合は値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値を表示。|
|日付（開始、完了含む ）|表示しない。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$POWER関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6793ded57dd74f4db4916814f1a3e375.png)

### パラメータ

![$POWER関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/882ad9f720da4d1a9e37a02dc00f7ea9.png)

### 計算結果

![$POWER関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/39f7feab0c2e449aa649efeaa7d79dff.png)