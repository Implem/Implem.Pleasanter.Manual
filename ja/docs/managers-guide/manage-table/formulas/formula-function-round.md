---
title: $ROUND関数
category: 計算式
order: '1380'
status: ''
parts: ''
urlstring: formula-function-round
translationKey: formula-function-round
shortname: $ROUND関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

数値を指定した桁数に四捨五入した値を返します。

## 構文

```
$ROUND(数値, 桁数)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|数値|半角数値|必須|四捨五入の対象とする数値。|
|桁数|半角数値|必須|数値を四捨五入した結果の桁数。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|数値|〇|〇|×|〇|×|
|桁数|〇|〇|×|〇|×|

## 戻り値

指定した桁数で四捨五入した数値。

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

![$ROUND関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/b3cafa3f54c64e0baec2d57d64c3a7e2.png)

### パラメータ

![$ROUND関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/52f6e06362ad4db7945069e8974d451f.png)

### 計算結果

![$ROUND関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/8b82c9c91bce491a9dda63d3f790ce57.png)

## 使用例②

小数点一位に四捨五入

### 計算式

![$ROUND関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/b3cafa3f54c64e0baec2d57d64c3a7e2.png)

### パラメータ

![$ROUND関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/637aa6af2f8a4bb5aa0c53ba5ea34172.png)

### 計算結果

![$ROUND関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/fa16e92e29e14f76b1861bef169877b0.png)
