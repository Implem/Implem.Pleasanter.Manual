---
title: $ISTEXT関数
category: 計算式
order: '1360'
status: ''
parts: ''
urlstring: formula-function-istext
translationKey: formula-function-istext
shortname: $ISTEXT関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

引数が文字列の場合にtrueを返します。

## 構文

```
$ISTEXT(文字列)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|文字列|任意の文字列|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|文字列|〇※1|〇※2|〇※2|〇※1|〇※2|

※1：入力値で以下のように判定

|入力値|結果|
|:---|:---|
|空欄|false|
|半角数値のみ|false|
|全角数値|true|
|その他文字列|true|

※2：必ずfalse

## 戻り値

文字列の場合、true。そうでない場合はfalse

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

![$ISTEXT関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/2148555d676d46c889ebbc3cfb679df8.png)

### パラメータ

![$ISTEXT関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/2a528e9f34aa43f5ab86ed05c187c6cc.png)

### 計算結果

![$ISTEXT関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/29f51a338c98483d8882dce84ddf55a8.png)