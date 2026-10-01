---
title: $LOWER関数
category: 計算式
order: '1190'
status: ''
parts: ''
urlstring: formula-function-lower
translationKey: formula-function-lower
shortname: $LOWER関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

文字列に含まれる英大文字を英小文字に変換します。

## 構文

```
$LOWER(文字列)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|文字列|任意の文字列|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|文字列|〇|〇|〇|〇|×|

## 戻り値

英大文字を英小文字に変換した文字列。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。戻り値が半角数値の場合でかつ値付きドロップダウンリストの場合は値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値が半角数値の場合に限り戻り値を表示。|
|日付（開始、完了含む ）|戻り値が日付形式の文字列の場合に限り戻り値を表示。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$LOWER関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/99f5259a6c90400eb2ecf87c2ba05923.png)

### パラメータ

![$LOWER関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/be8a2e20e3464b8daeba8181512dd0ce.png)

### 計算結果

![$LOWER関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/aade88979de14cb4ac178b3a9f9cfa9a.png)