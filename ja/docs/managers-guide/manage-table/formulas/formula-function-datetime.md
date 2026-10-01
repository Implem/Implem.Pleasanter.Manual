---
title: $DATETIME関数
category: 計算式
order: '1025'
status: ''
parts: ''
urlstring: formula-function-datetime
translationKey: formula-function-datetime
shortname: $DATETIME関数
created: 2023-12-29
updated: 2024-06-07
---

## 概要

指定した年、月、日、時、分、秒の日時を求めます。

## 構文

```
$DATETIME(年,月,日,時,分,秒)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|年|4桁の半角数値|必須|1900以上を指定。1900未満の場合はエラー。半角数値以外の文字列の場合はエラー。|
|月|半角数値|必須|1～12以外を入力した場合は入力値で過去月or未来月を計算。半角数値以外の文字列の場合はエラー。空白は0と判定。|
|日|半角数値|必須|1～31以外を入力した場合は入力値で過去日or未来日を計算。半角数値以外の文字列の場合はエラー。空白は0と判定。|
|時|半角数値|必須|1～23以外を入力した場合は入力値で過去日or未来日を計算。半角数値以外の文字列の場合はエラー。空白は0と判定。|
|分|半角数値|必須|1～59以外を入力した場合は入力値で過去日or未来日を計算。半角数値以外の文字列の場合はエラー。空白は0と判定。|
|秒|半角数値|必須|1～59以外を入力した場合は入力値で過去日or未来日を計算。半角数値以外の文字列の場合はエラー。空白は0と判定。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|年|〇|〇|×|〇|×|
|月|〇|〇|×|〇|×|
|日|〇|〇|×|〇|×|
|時|〇|〇|×|〇|×|
|分|〇|〇|×|〇|×|
|秒|〇|〇|×|〇|×|

## 戻り値

`yyyy/MM/dd hh:mm:ss` 形式の日時。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。|
|数値（作業量、進捗率、残作業量含む）|表示しない。|
|日付（開始、完了含む ）|戻り値を表示。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$DATETIME関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/ed173335530e4b428b642adc9cb31fde.png)

### パラメータ

![$DATETIME関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c57aa668522e4b08a790e3ed8d5fdb52.png)

### 計算結果

![$DATETIME関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/fdc43f5f94df47b0befb38f1003a735f.png)

## 使用例②

月が0の場合

### パラメータ

![$DATETIME関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a6cb97ba9134404d8bc9c4d8b92e93b3.png)

### 計算結果

![$DATETIME関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/b141fb7d4e5f494184b57430f5b6fe24.png)

## 使用例③

日がマイナス値の場合

### パラメータ

![$DATETIME関数の使用例③で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/755b2e34041c4a08aa4eb6004837c561.png)

### 計算結果

![$DATETIME関数の使用例③の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/15c5ed548bb44ccf8d9a95c62d0d2e5c.png)

## 使用例④

時が23を超える場合

### パラメータ

![$DATETIME関数の使用例④で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c6b4b50d8a514e9a9fb23e244b84269e.png)

### 計算結果

![$DATETIME関数の使用例④の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/724268a506dd42358b0baa23c3ecd821.png)

## 使用例⑤

分がマイナス値の場合

### パラメータ

![$DATETIME関数の使用例⑤で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/bab162287bfc4fc381f9c3d01a655984.png)

### 計算結果

![$DATETIME関数の使用例⑤の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/d05ee9c75fc643d3b486c0101a150f9a.png)
