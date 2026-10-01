---
title: $ROUNDDOWN関数
category: 計算式
order: '1390'
status: ''
parts: ''
urlstring: formula-function-rounddown
translationKey: formula-function-rounddown
shortname: $ROUNDDOWN関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

数値を指定した桁数で切り捨てた値を返します。

## 構文

```
$ROUNDDOWN(数値, 桁数)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|数値|半角数値|必須|切り捨ての対象とする数値。|
|桁数|半角数値|必須|数値を切り捨てた結果の桁数。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|数値|〇|〇|×|〇|×|
|桁数|〇|〇|×|〇|×|

## 戻り値

指定した桁数で切り捨てた数値。

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

![$ROUNDDOWN関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/b1accc9bfd444ab49d27d6965caffdde.png)

### パラメータ

![$ROUNDDOWN関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/7e9380035c6d4dbd91e3c25322cf9bf3.png)

### 計算結果

![$ROUNDDOWN関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/41b41671ab1d47b6a4c6767518507876.png)

## 使用例②

小数点一位となるように切り捨て

### 計算式

![$ROUNDDOWN関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/b1accc9bfd444ab49d27d6965caffdde.png)

### パラメータ

![$ROUNDDOWN関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a5d31af8ad1144bdb8e2d196d3e93e4e.png)

### 計算結果

![$ROUNDDOWN関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/16208e2baa01403f8186e8ce50a42f23.png)
