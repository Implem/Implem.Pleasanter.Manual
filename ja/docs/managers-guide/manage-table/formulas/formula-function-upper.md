---
title: $UPPER関数
category: 計算式
order: '1260'
status: ''
parts: ''
urlstring: formula-function-upper
translationKey: formula-function-upper
shortname: $UPPER関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

文字列に含まれる英小文字を英大文字に変換します。

## 構文

```
$UPPER(文字列)  
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

英小文字を英大文字に変換した文字列。

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

![$UPPER関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/197f5de240a34937b7d776ab38762585.png)

### パラメータ

![$UPPER関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6e6f9d2a4cac416faba9c72210373ac0.png)

### 計算結果

![$UPPER関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/f27b72fcb5804e60929ab8ad0b0defff.png)