---
title: $MINUTE関数
category: 計算式
order: '1060'
status: ''
parts: ''
urlstring: formula-function-minute
translationKey: formula-function-minute
shortname: $MINUTE関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

指定した日付の分数を求めます。

## 構文

```
$MINUTE(日付) 
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

分数（0～59）。

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

![$MINUTE関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/e33059f95bb84a198faba4b5d52252cf.png)

### パラメータ

![$MINUTE関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/1822ea4d1a2a4e28a80f6874a54b219d.png)

### 計算結果

![$MINUTE関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/593a8231cc81401ea9d2e689827626f8.png)