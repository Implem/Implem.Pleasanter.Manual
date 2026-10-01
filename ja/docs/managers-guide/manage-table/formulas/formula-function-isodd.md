---
title: $ISODD関数
category: 計算式
order: '1350'
status: ''
parts: ''
urlstring: formula-function-isodd
translationKey: formula-function-isodd
shortname: $ISODD関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

引数が奇数の場合にtrueを返します。

## 構文

```
$ISODD(数値)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|数値|半角数値|必須|半角数値以外はエラー|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|数値|〇|〇|×|〇|×|

## 戻り値

引数が奇数の場合、true。そうでない場合はfalse。

### 対象とする項目に対する戻り値

|対象|戻り値|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|"True"または"False"という文字列を表示|
|数値（作業量、進捗率、残作業量含む）|表示しない|
|日付（開始、完了含む ）|表示しない|
|説明（内容含む）|"True"または"False"という文字列を表示|
|チェック（ロック含む）|trueの場合チェックON、falseの場合チェックOFF|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$ISODD関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/23e2374556ee443aa81122e65267b5d9.png)

### パラメータ

![$ISODD関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/da07fc85d5bc4a059d03c371522af723.png)

### 計算結果

![$ISODD関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/80cd03102d5a41fa97c1f72fa506fccd.png)