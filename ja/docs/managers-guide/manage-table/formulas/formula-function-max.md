---
title: $MAX関数
category: 計算式
order: '1430'
status: ''
parts: ''
urlstring: formula-function-max
translationKey: formula-function-max
shortname: $MAX関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

引数の最大値を求めます。

## 構文

```
$MAX(数値1, [数値2],...)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|数値1|半角数値|必須|最大値を求める1つ目の数値。|
|[数値2],...|半角数値|任意|最大値を求める追加する数値。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|数値1|〇|〇|×|〇|×|
|[数値2]|〇|〇|×|〇|×|

## 戻り値

引数の最大値。
引数にエラー値または数値に変換できない文字列を指定すると、エラーになります。

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

![$MAX関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/dc506a1b8d5d4da3933e2eabb8b07350.png)

### パラメータ

![$MAX関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/8a6a797a56244d50b13e06d356cfd92d.png)

### 計算結果

![$MAX関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/da050a1dad024d58b09842b2fb7c9994.png)