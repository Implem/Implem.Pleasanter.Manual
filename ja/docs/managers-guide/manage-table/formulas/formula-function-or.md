---
title: $OR関数
category: 計算式
order: '1320'
status: ''
parts: ''
urlstring: formula-function-or
translationKey: formula-function-or
shortname: $OR関数
created: 2023-12-06
updated: 2024-06-12
---

## 概要

いずれかの引数がtrueの場合にtrueを返します。

## 構文

```
$OR(論理式1,[論理式2],...)
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

引数いずれかがtrueの場合、true。全てfalseの場合、false。

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

![$OR関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/dd71c0ba896145babd2fa17d70f154ac.png)

### パラメータ

![$OR関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/359c0faf2d0c405690c796d1dd5d1feb.png)

### 計算結果

![$OR関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/11157cf3eb98407f9d56ea4e95a034dd.png)

## 使用例②

パラメータを複数指定

### 計算式

![$OR関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/4cf345ebaf6b4561b5b83c3627a899c7.png)

### パラメータ

![$OR関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/3aa786a7f3514864aeed04f408a53c9a.png)

### 計算結果

![$OR関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a43c1693954141f091fd99f240e0ca0b.png)