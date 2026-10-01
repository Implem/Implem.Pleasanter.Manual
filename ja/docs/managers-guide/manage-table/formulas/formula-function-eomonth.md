---
title: $EOMONTH関数
category: 計算式
order: '1045'
status: ''
parts: ''
urlstring: formula-function-eomonth
translationKey: formula-function-eomonth
shortname: $EOMONTH関数
created: 2023-12-27
updated: 2024-06-07
---

## 概要

開始日から起算して指定された月数の前または後の月の最終日を求めます。

## 構文

```
$EOMONTH(開始日,月)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|開始日|yyyy/mm/d形式の日付または日付文字列|必須||
|月|半角数値|必須|正の数を指定した場合は起算日より後の日付、負の数を指定した場合は起算日より前の日付を返却|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|開始日|〇|×|〇|〇|×|
|月|〇|〇|×|〇|×|

## 戻り値

yyyy/mm/dd形式の日付。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。|
|数値（作業量、進捗率、残作業量含む）|表示しない。|
|日付（開始、完了含む ）|戻り値を表示。エディタの書式が「日付と時刻（分）」、「日付と時刻（秒）」の場合は00:00:00を自動補完。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$EOMONTH関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/260960c7df954ebfab5c4ba0b3cb252f.png)

### パラメータ

![$EOMONTH関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/3b4b4c77813b4fc7aba631273176a84d.png)

### 計算結果

![$EOMONTH関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/e35dafad69e3472ab2e983441069315b.png)

