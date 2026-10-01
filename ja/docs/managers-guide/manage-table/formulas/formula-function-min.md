---
title: $MIN関数
category: 計算式
order: '1440'
status: ''
parts: ''
urlstring: formula-function-min
translationKey: formula-function-min
shortname: $MIN関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

引数の最小値を求めます。

## 構文

```
$MIN(数値1, [数値2],...)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|数値1|半角数値|必須|最小値を求める1つ目の数値。|
|[数値2],...|半角数値|任意|最小値を求める追加する数値。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|数値1|〇|〇|×|〇|×|
|[数値2]|〇|〇|×|〇|×|

## 戻り値

引数の最小値。
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

![$MIN関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/044102e804ea42768ba4d420b82065ec.png)

### パラメータ

![$MIN関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/819155947bd948cba9352092befcb558.png)

### 計算結果

![$MIN関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/e40c9669ef4f4ea2aac4bc869efab742.png)