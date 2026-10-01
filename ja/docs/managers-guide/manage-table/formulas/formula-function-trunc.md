---
title: $TRUNC関数
category: 計算式
order: '1410'
status: ''
parts: ''
urlstring: formula-function-trunc
translationKey: formula-function-trunc
shortname: $TRUNC関数
created: 2023-12-06
updated: 2024-06-12
---

## 概要

数値の小数部を指定した桁数で切り捨てた値を返します。

## 構文

```
$TRUNC(数値, [桁数])
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|数値|半角数値|必須|小数部を切り捨てる数値。|
|[桁数]|半角数値|任意|切り捨てを行った後の桁数を指定。省略時は0を指定したとみなす。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|数値|〇|〇|×|〇|×|
|[桁数]|〇|〇|×|〇|×|

## 戻り値

小数点を指定した桁数で切り捨てた数値。

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

![$TRUNC関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/55a22f32c93b4d54bc7f3c59fe6bb37c.png)

### パラメータ

![$TRUNC関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/26297517159e43b7a1112be8701d7842.png)

### 計算結果

![$TRUNC関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/aa7040adaaa049d096bc5644c1c2ca0d.png)

## 使用例②

パラメータ[桁数]を指定

### 計算式

![$TRUNC関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/98d3b56f15c2495f98aa92981e231ba1.png)

### パラメータ

![$TRUNC関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/34c4ea8c6dbf400fb7155308bfef4b6e.png)

### 計算結果

![$TRUNC関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c0590d1139fe4c159851898c70e76453.png)