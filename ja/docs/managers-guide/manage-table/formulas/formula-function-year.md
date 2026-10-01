---
title: $YEAR関数
category: 計算式
order: '1120'
status: ''
parts: ''
urlstring: formula-function-year
translationKey: formula-function-year
shortname: $YEAR関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

指定した日付の年数を求めます。

## 構文

```
$YEAR(日付) 
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|日付|yyyy/mm/dd形式またはyyyy/mm/dd hh:MM:ss形式の日付または日付文字列|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|日付|〇|×|〇|〇|×|

## 戻り値

年数。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値を表示。|
|日付（開始、完了含む ）|表示しない。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$YEAR関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/ba87e325e1194a9f8d5230f18bd4408c.png)

### パラメータ

![$YEAR関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/00ceecba66de47b8a12cf67c41865d6a.png)

### 計算結果

![$YEAR関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/dee7f99fc8b34ecbbc385c2c277e17c1.png)
