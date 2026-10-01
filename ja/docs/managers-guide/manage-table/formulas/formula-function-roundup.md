---
title: $ROUNDUP関数
category: 計算式
order: '1400'
status: ''
parts: ''
urlstring: formula-function-roundup
translationKey: formula-function-roundup
shortname: $ROUNDUP関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

数値を指定した桁数で切り上げた値を返します。

## 構文

```
$ROUNDUP(数値, 桁数)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|数値|半角数値|必須|切り上げの対象とする数値。|
|桁数|半角数値|必須|数値を切り上げた結果の桁数。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|数値|〇|〇|×|〇|×|
|桁数|〇|〇|×|〇|×|

## 戻り値

指定した桁数で切り上げた数値。

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

![$ROUNDUP関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6eafcf986aac44c3b3d3afdf7b038e91.png)

### パラメータ

![$ROUNDUP関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/5856477b748c41d0bd70604e9efb2778.png)

### 計算結果

![$ROUNDUP関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/e09a0468005045bf916e651989174be7.png)

## 使用例②

小数点一位となるように切り捨て

### 計算式

![$ROUNDUP関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6eafcf986aac44c3b3d3afdf7b038e91.png)

### パラメータ

![$ROUNDUP関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/55c85ce52125420da9de90938a0d3ef8.png)

### 計算結果

![$ROUNDUP関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a88f1b40ce574ae687e75db2a4c05c90.png)