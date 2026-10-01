---
title: $ISBLANK関数
category: 計算式
order: '1325'
status: ''
parts: ''
urlstring: formula-function-isblank
translationKey: formula-function-isblank
shortname: $ISBLANK関数
created: 2023-12-27
updated: 2024-06-07
---

## 概要

引数が空欄の場合にtrueを返します。

## 構文

```
$ISBLANK(文字列)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|文字列|任意の文字列|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|文字列|〇|〇|〇|〇|〇※1|

※1：必ずfalse

## 戻り値

空欄の場合true。そうでない場合はfalse

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

![$ISBLANK関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/e24b75f3953544f1b6a9b9bf9473d26f.png)

### パラメータ

![$ISBLANK関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/4e899067906c47398fd4aa20b6196f20.png)

### 計算結果

![$ISBLANK関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/8ee0c99e4be646108548d03b4462d0dd.png)