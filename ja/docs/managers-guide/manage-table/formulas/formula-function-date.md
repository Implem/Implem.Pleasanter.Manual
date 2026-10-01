---
title: $DATE関数
category: 計算式
order: '1010'
status: ''
parts: ''
urlstring: formula-function-date
translationKey: formula-function-date
shortname: $DATE関数
created: 2023-12-05
updated: 2024-06-12
---

## 概要

指定した年、月、日の日付を求めます。

## 構文

```
$DATE(年,月,日)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|年|4桁の半角数値|必須|1900以上を指定。1900未満の場合はエラー。半角数値以外の文字列の場合はエラー。|
|月|半角数値|必須|1～12以外を入力した場合は入力値で過去月or未来月を計算。半角数値以外の文字列の場合はエラー。空白は0と判定。|
|日|半角数値|必須|1～31以外を入力した場合は入力値で過去日or未来日を計算。半角数値以外の文字列の場合はエラー。空白は0と判定。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|年|〇|〇|×|〇|×|
|月|〇|〇|×|〇|×|
|日|〇|〇|×|〇|×|

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

![$DATE関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/00db6c15e46f4ccdb6b139145e251f0e.png)

### パラメータ

![$DATE関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/e6b0c88220934afe9f1424d0816bb557.png)

### 計算結果

エディタの書式：年月日
![$DATE関数の使用例①の計算結果（エディタの書式：年月日）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/f9192a4391be4e8fa4d7da7de65ad7a2.png)
エディタの書式：日付と時刻（秒）
![$DATE関数の使用例①の計算結果（エディタの書式：日付と時刻（秒））](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c94ecee1a08247168a56b1651eb5c6d7.png)

## 使用例②

月が0の場合

### パラメータ

![$DATE関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a58357bbb5ed4368a5fd786744d31612.png)

### 計算結果

![$DATE関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/59a7308f0d124fab88838fd6ab251b8e.png)

## 使用例③

日がマイナス値の場合

### パラメータ

![$DATE関数の使用例③で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c550902a39484f2ca186ede72311450a.png)

### 計算結果

![$DATE関数の使用例③の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/3665d41fa54e4c3e926b990d8dd59228.png)
