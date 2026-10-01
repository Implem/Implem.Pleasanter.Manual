---
title: $NOT関数
category: 計算式
order: '1310'
status: ''
parts: ''
urlstring: formula-function-not
translationKey: formula-function-not
shortname: $NOT関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

引数がtrueの場合にfalseを返します。

## 構文

```
$NOT(論理式)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|論理式|「論理式」|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|論理式|〇※1|〇※1|〇※1|〇※1|〇|

※1：「論理式」を構成する変数として利用可能。
例)
数値A == 1000
日付A > 日付B
分類A == "テキスト"

## 戻り値

引数がtrueの場合、false。そうでない場合はtrue。

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

![$NOT関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/1bdefea320ed4adaa0e84e0afad63fec.png)

### パラメータ

![$NOT関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/e48b992ebf3e4683b913400ae4369f81.png)

### 計算結果

![$NOT関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/633a4e268a194a2482799de73004929e.png)

## 使用例②

パラメータに論理式を指定

### 計算式

![$NOT関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/940590eb54bc4753888e40f1969ea090.png)

### パラメータ

![$NOT関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/4ec9ab2e93f843f2ab242fefe1a0e174.png)

### 計算結果

![$NOT関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a10fd99cae8240d69e24fb56811705da.png)
