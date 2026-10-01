---
title: $FIND関数
category: 計算式
order: '1150'
status: ''
parts: ''
urlstring: formula-function-find
translationKey: formula-function-find
shortname: $FIND関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

検索文字列を対象の文字列の中で検索し、検索文字列が最初に現れる位置を左端から数えた結果を求めます。検索は大文字小文字は区別されます。ワイルドカード文字は使用できません。

## 構文

```
$FIND(検索文字列,対象の文字列,[開始位置])
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|検索文字列|任意の文字列|必須||
|対象の文字列|任意の文字列|必須||
|開始位置|半角数値。1以上の整数|任意|検索を開始する位置を指定。「対象の文字列」の先頭文字から検索を行う場合は1を指定。省略時は1を指定したとみなす。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|検索文字列|〇|〇|〇|〇|×|
|対象の文字列|〇|〇|〇|〇|×|
|[開始位置]|〇|〇|×|〇|×|

## 戻り値

検索文字列が最初に現れた位置（1以上の整数）。
検索文字列が見つからなかった場合はエラーとなります。
開始位置が対象の文字列の文字数より大きい場合はエラーとなります。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示|
|数値（作業量、進捗率、残作業量含む）|戻り値を表示|
|日付（開始、完了含む ）|表示しない|
|説明（内容含む）|戻り値を表示|
|チェック（ロック含む）|表示しない|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$FIND関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6cfcdb5305a04d3d96dff3be148d9ef4.png)

### パラメータ

![$FIND関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6183b8cd64fb40aba24f75d9e3897305.png)

### 計算結果

![$FIND関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/8ec740bb31fb4a7cb75b5c6cfb5ad1f2.png)

## 使用例②

パラメータ[開始位置]を指定

### 計算式

![$FIND関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/be7dbb6908d846e09c2c34616a4bab17.png)

### パラメータ

![$FIND関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/fa7aff4670b6486ebc36484114d3e8a6.png)

### 計算結果

![$FIND関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/3f86e0281f88473f8fa7f16cce1a9e06.png)