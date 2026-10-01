---
title: $MOD関数
category: 計算式
order: '1370'
status: ''
parts: ''
urlstring: formula-function-mod
translationKey: formula-function-mod
shortname: $MOD関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

数値を除算した剰余を返します。

## 構文

```
$MOD(数値, 除数)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|数値|半角数値|必須|除算の分子。|
|除数|半角数値|必須|除算の分母。0を指定した場合はエラー。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|数値|〇|〇|×|〇|×|
|除数|〇|〇|×|〇|×|

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

![$MOD関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/0d5b3c98eaa045e9ad08df885403a3eb.png)

### パラメータ

![$MOD関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/fb8da14dccb64fc78c69697c2171aa92.png)

### 計算結果

![$MOD関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/d97bb781effc499ca3f9aa31da9aaab4.png)