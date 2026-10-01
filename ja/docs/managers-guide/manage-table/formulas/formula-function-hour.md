---
title: $HOUR関数
category: 計算式
order: '1050'
status: ''
parts: ''
urlstring: formula-function-hour
translationKey: formula-function-hour
shortname: $HOUR関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

指定した日付の時間数を求めます。

## 構文

```
$HOUR(日付) 
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|日付|yyyy/mm/dd形式またはyyyy/mm/dd hh:MM:ss形式の日付または日付文字列|必須|yyyy/mm/dd形式の場合は「00:00:00」を自動補完する。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|日付|〇|×|〇|〇|×|

## 戻り値

時間数（0～23）。

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

![$HOUR関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/3060d130b0a34721bcbf452337e7b3c7.png)

### パラメータ

![$HOUR関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/ddd426b0e8d04db7997283e5565cf587.png)

### 計算結果

![$HOUR関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/2c6b66f225f74d0f94bb4a4699d5ed02.png)