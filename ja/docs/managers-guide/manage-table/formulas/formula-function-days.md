---
title: $DAYS関数
category: 計算式
order: '1040'
status: ''
parts: ''
urlstring: formula-function-days
translationKey: formula-function-days
shortname: $DAYS関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

2つの日付間の日数を求めます。

## 構文

```
$DAYS(終了日,開始日)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|終了日|yyyy/mm/d形式の日付または日付文字列|必須|開始日＞終了日の場合エラー。|
|開始日|yyyy/mm/d形式の日付または日付文字列|必須|開始日＞終了日の場合エラー。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|終了日|〇|×|〇|〇|×|
|開始日|〇|×|〇|〇|×|

## 戻り値

日数。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示|
|数値（作業量、進捗率、残作業量含む）|戻り値を表示。|
|日付（開始、完了含む ）|表示しない。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$DAYS関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/8b39098c8afc4d94b8638463f2adf217.png)

### パラメータ

![$DAYS関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/37a929de3e514a80994f6f8da8ca2cf8.png)

### 計算結果

![$DAYS関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/75e3f80f653147a5b8a8ef3a2588b373.png)