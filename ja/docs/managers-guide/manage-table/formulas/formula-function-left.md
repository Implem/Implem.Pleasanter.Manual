---
title: $LEFT関数
category: 計算式
order: '1170'
status: ''
parts: ''
urlstring: formula-function-left
translationKey: formula-function-left
shortname: $LEFT関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

文字列の先頭から指定された数の文字を返します。

## 構文

```
$LEFT(文字列,[文字数])
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|文字列|任意の文字列|必須||
|[文字数]|半角数値。0以上の整数|任意|取り出す文字数を指定。省略時は1を指定したとみなす。0を指定した場合は空文字を返す。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|文字列|〇|〇|〇|〇|×|
|[文字数]|〇|〇|×|〇|×|

## 戻り値

取り出した文字列。
[文字数]が文字列の文字数より大きい場合は文字列全体を返します。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。戻り値が半角数値の場合でかつ値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値が半角数値の場合に限り戻り値を表示。|
|日付（開始、完了含む ）|戻り値が日付形式の文字列の場合に限り戻り値を表示。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$LEFT関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/8be290f37fb34cd29ff50569653f7e9a.png)

### パラメータ

![$LEFT関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/897004d5f3134b49b6320ea8cebae4e5.png)

### 計算結果

![$LEFT関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/d58e85696c37419e9629f2e0649e9d6d.png)

## 使用例②

パラメータ[文字数]を指定

### 計算式

![$LEFT関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/f0ccdfa00113484a885d531b927d70a9.png)

### パラメータ

![$LEFT関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6cb5e02c9d0e43d28fd54564fa953142.png)

### 計算結果

![$LEFT関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/7410464995284d528c0ec12a14ff47f1.png)

