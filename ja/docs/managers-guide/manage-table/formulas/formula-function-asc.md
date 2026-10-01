---
title: $ASC関数
category: 計算式
order: '1130'
status: ''
parts: ''
urlstring: formula-function-asc
translationKey: formula-function-asc
shortname: $ASC関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

全角文字を半角文字に変換します。

## 構文

```
$ASC(文字列)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|文字列|任意の文字列|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|文字列|〇|〇|〇|〇|〇|

## 戻り値

全角文字を半角文字に変換した文字列。
引数にチェック項目を指定した場合は文字列"true"または"false"を返却する。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。|
|数値（作業量、進捗率、残作業量含む）|表示しない。|
|日付（開始、完了含む ）|表示しない。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$ASC関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c959db330275409db3ace89ebe60f16a.png)

### パラメータ

![$ASC関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c034b1bdf1d74cc7a9ec4aa07c9e29e1.png)

### 計算結果

![$ASC関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/4a95bed5800d4a28bc076b050bbe865d.png)

## 使用例②

パラメータにチェック項目を指定

### 計算式

![$ASC関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/e193a268a70f4878b74faba4f500c721.png)

### パラメータ

![$ASC関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/de015d5e7a59406ea9cf29286a4398a5.png)

### 計算結果

![$ASC関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/0d420cfc1e104cc086377033a63d0c86.png)

