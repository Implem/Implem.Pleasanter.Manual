---
title: $ISNUMBER関数
category: 計算式
order: '1340'
status: ''
parts: ''
urlstring: formula-function-isnumber
translationKey: formula-function-isnumber
shortname: $ISNUMBER
created: 2023-12-06
updated: 2024-06-07
---

## 概要

引数が数値の場合にtrueを返します。

## 構文

```
$ISNUMBER(文字列)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|文字列|任意の文字列|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|文字列|〇※1|〇※2|〇※3|〇※1|〇※3|

※1：入力値で以下のように結果を返却

|入力値|結果|
|:---|:---|
|空欄|false|
|半角数値のみ|true|
|全角数値|false|
|その他文字列|false|

※2：必ずtrueを返却
※3：必ずfalseを返却

## 戻り値

数値の場合、true。そうでない場合はfalse

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

![$ISNUMBER関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a33b94448fbe4c89837de4b67f8ce63d.png)

### パラメータ

![$ISNUMBER関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/2b518dda4b144e7496dbdca36a623611.png)

### 計算結果

![$ISNUMBER関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/5f4673581f1f49e3bbf5df29a85da121.png)