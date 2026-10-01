---
title: $MID関数
category: 計算式
order: '1200'
status: ''
parts: ''
urlstring: formula-function-mid
translationKey: formula-function-mid
shortname: $MID関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

文字列の指定位置から指定された数の文字を返します。

## 構文

```
$MID(文字列,開始位置,文字数)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|文字列|任意の文字列|必須||
|開始位置|半角数値。1以上の整数|必須||
|文字数|半角数値。0以上の整数|必須|取り出す文字数を指定。0を指定した場合は空文字を返す。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|文字列|〇|〇|〇|〇|×|
|開始位置|〇|〇|×|〇|×|
|文字数|〇|〇|×|〇|×|

## 戻り値

取り出した文字。
開始位置が文字列の長さより大きい場合は空文字を返す。
文字数が文字列の長さより大きい場合は文字列末尾までの文字を返す。

### 対象とする項目に対する戻り値

|対象|戻り値|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。戻り値が半角数値の場合でかつ値付きドロップダウンリストの場合は値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値が半角数値の場合に限り戻り値を表示。|
|日付（開始、完了含む ）|戻り値が日付形式の文字列の場合に限り戻り値を表示。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$MID関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6427b509f27047798eb02ac59f5077f1.png)

### パラメータ

![$MID関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/5caf2b7d82c04193a31ebd9193971be9.png)

### 計算結果

![$MID関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/cbb86b2dc4f645aaaf239842859a988a.png)