---
title: $IF関数
category: 計算式
order: '1290'
status: ''
parts: ''
urlstring: formula-function-if
translationKey: formula-function-if
shortname: $IF関数
created: 2023-12-06
updated: 2024-06-12
---

## 概要

「論理式」の結果（trueかfalse）に応じて、指定された値を返します。

## 構文

```
$IF(論理式,計算式1,計算式2)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|論理式|「論理式」|必須||
|計算式1|計算式|必須|「論理式」がtrueの場合に実行する計算式|
|計算式2|計算式|必須|「論理式」がfalseの場合に実行する計算式|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|論理式|〇※1|〇※1|〇※1|〇※1|〇|
|計算式1|〇|〇|〇|〇|〇|
|計算式2|〇|〇|〇|〇|〇|

※1：「論理式」を構成する変数として利用可能。
例)
数値A == 1000
日付A > 日付B
分類A == "テキスト"

## 戻り値

論理式がtrueの場合は計算式1の結果を返却し、falseの場合は計算式2の結果を返却する。

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

![$IF関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6138742adba149538a304fd144fa241a.png)

### パラメータ

![$IF関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/97ea2ed10fe647499fa8868586dcd8fc.png)

### 計算結果

![$IF関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/387a0ce0386a430a9b455ae1ff78c218.png)

## 使用例②

分類Aの値が「割引」の場合に70%割引した値を計算

### 計算式

![$IF関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/bc1acda183284d77a7d0511dc3ef0439.png)

### パラメータ

![$IF関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/b6fbfcdafc7c4b77b6e5ae4f223073c1.png)

### 計算結果

![$IF関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/7973ec796d414ce28f53c3bb5b206315.png)