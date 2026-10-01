---
title: $TRIM関数
category: 計算式
order: '1250'
status: ''
parts: ''
urlstring: formula-function-trim
translationKey: formula-function-trim
shortname: $TRIM関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

文字列の前後の不要なスペースを取り除きます。文字列内のスペースは取り除きません。

## 構文

```
$TRIM(文字列)
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

文字列の前後のスペースを取り除いた文字列。

### 対象とする項目に対する戻り値

|対象|戻り値|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値が半角数値の場合に限り戻り値を表示。|
|日付（開始、完了含む ）|戻り値が日付形式の場合に限り戻り値を表示。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$TRIM関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/ce1cbe1307bb42c5933545be18f5287a.png)

### パラメータ

![$TRIM関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/f86cac2fc7c748be86413f9e43c125a9.png)

### 計算結果

![$TRIM関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/ac05e98ab01f4627a8749bcae0f709b3.png)
