---
title: $TEXT関数
category: 計算式
order: '1245'
status: ''
parts: ''
urlstring: formula-function-text
translationKey: formula-function-text
shortname: $TEXT関数
created: 2023-12-27
updated: 2024-06-12
---

## 概要

表示形式を適用した文字列に変換します。

## 構文

```
$TEXT(値, 表示形式)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|値|任意の文字列|必須||
|表示形式|[C#で利用可能な書式指定文字列](https://learn.microsoft.com/ja-jp/dotnet/standard/base-types/formatting-types)|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|値|〇|〇|〇|〇|×|
|表示形式|〇|×|×|〇|×|

## 戻り値

表示形式を適用した文字列。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。戻り値が半角数値の場合でかつ値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値が半角数値の場合に限り戻り値を表示。|
|日付（開始、完了含む ）|戻り値が日付形式の場合に限り戻り値を表示。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

数値を桁区切り表示
分類Aの表示形式を指定することで、数値Aを桁区切り表示に置き換えて分類Bに計算結果として出力します。

### 計算式

![$TEXT関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/97151912dce848f9a50a90d93d98e055.png)

### パラメータ

![$TEXT関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/88e197f842c14a3d9b316b10286ecc09.png)

### 計算結果

![$TEXT関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6625fc73138c41628fac732c2972362b.png)

## 使用例②

数値を通貨（円）表示
分類Aの表示形式を指定することで、通貨記号＋数値Aの桁区切り表示で分類Bに計算結果として出力します。「\」をエスケープさせるために「\\」と指定します。

### 計算式

![$TEXT関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/7a2272e3953e451b89935f540d4772c1.png)

### パラメータ

![$TEXT関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/507c25c328404bf68e270d8f042927b8.png)

### 計算結果

![$TEXT関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/bef22e7c8d4e494095f592321e724ae6.png)

## 使用例③

日付を年月日曜日表示
分類Aの表示形式を指定することで、日付Aを年月日曜日表示に置き換えて分類Bに計算結果として出力します。

### 計算式

![$TEXT関数を使った使用例③の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/e6b503a1fe8342b0bca08b39b813f794.png)

### パラメータ

![$TEXT関数の使用例③で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/1570ca5945b14601bb6f22dae3b5e0ba.png)

### 計算結果

![$TEXT関数の使用例③の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/1f139b8f6aab4d4ab5d439caa666ff74.png)