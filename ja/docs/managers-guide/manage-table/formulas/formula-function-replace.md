---
title: $REPLACE関数
category: 計算式
order: '1210'
status: ''
parts: ''
urlstring: formula-function-replace
translationKey: formula-function-replace
shortname: $REPLACE関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

対象の文字列に対して指定した文字数の文字を別の文字に変換します。

## 構文

```
$REPLACE(対象の文字列,開始位置,文字数,置換文字列) 
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|対象の文字列|任意の文字列|必須||
|開始位置|半角数値。1以上の整数|必須|置換文字列と置き換える先頭文字の位置を指定。先頭文字が1になる。|
|文字数|半角数値。1以上の整数|必須|置換文字列と置き換える文字数を指定。|
|置換文字列|任意の文字列|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|対象の文字列|〇|〇|〇|〇|×|
|開始位置|〇|〇|×|〇|×|
|文字数|〇|〇|×|〇|×|
|置換文字列|〇|〇|〇|〇|×|

## 戻り値

置換後の文字列。

### 対象とする項目に対する戻り値

|対象|戻り値|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。戻り値が半角数値の場合でかつ値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値が半角数値の場合に限り戻り値を表示。|
|日付（開始、完了含む ）|戻り値が日付形式の文字列の場合に限り戻り値を表示。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$REPLACE関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/9113a26e46d34b2e816c4bb2e2d211c1.png)

### パラメータ

![$REPLACE関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/ff8825f100cf4e1cb17ace33da7cf61b.png)

### 計算結果

![$REPLACE関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/32c0f540aae145219e8a611238e8d24b.png)