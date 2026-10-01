---
title: $AND関数
category: 計算式
order: '1280'
status: ''
parts: ''
urlstring: formula-function-and
translationKey: formula-function-and
shortname: $AND関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

全ての引数がtrueの場合にtrueを返します。

## 構文

```
$AND(論理式1,[論理式2],...)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|論理式1|「論理式」|必須||
|[論理式2],...|「論理式」|任意||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|論理式1|〇※1|〇※1|〇※1|〇※1|〇|

※1：「論理式」を構成する変数として利用可能。
例)
数値A == 1000
日付A > 日付B
分類A == "テキスト"

## 戻り値

引数全てがtrueの場合、true。そうでない場合はfalse

### 対象とする項目に対する戻り値

|対象|戻り値|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|"True"または"False"という文字列を表示|
|数値（作業量、進捗率、残作業量含む）|表示しない|
|日付（開始、完了含む ）|表示しない|
|説明（内容含む）|"True"または"False"という文字列を表示|
|チェック（ロック含む）|trueの場合チェックON、falseの場合チェックOFF|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$AND関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/7c8ccdb85ef3412bbbc6dbcdb90bf4a4.png)

### パラメータ

![$AND関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/b7587063712241afaa091e12f41069dc.png)

### 計算結果

![$AND関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/18cf14a2f1e54c689a4c5383026cd9fa.png)

## 使用例②

パラメータを複数設定

### 計算式

![$AND関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/f321ab3096b64b41950e87c92cf639ce.png)

### パラメータ

![$AND関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/26fb2137d7eb49d590fa9b32949f5a19.png)

### 計算結果

![$AND関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a736f091076e45b4929d19173beae47a.png)
