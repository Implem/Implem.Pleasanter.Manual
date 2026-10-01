---
title: $JIS関数
category: 計算式
order: '1160'
status: ''
parts: ''
urlstring: formula-function-jis
translationKey: formula-function-jis
shortname: $JIS関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

半角文字を全角文字に変換します。

## 構文

```
$JIS(文字列)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|文字列|任意の文字列|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|文字列|〇|〇|〇|〇|〇|

## 戻り値

半角文字を全角文字に変換した文字列。
引数にチェック項目を指定した場合は文字列"ｔｒｕｅ"または"ｆａｌｓｅ"を返却する。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。|
|数値（作業量、進捗率、残作業量含む）|表示しない。|
|日付（開始、完了含む ）|表示しない。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$JIS関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/904d373fd6454fa5b370b9ebfe65a906.png)

### パラメータ

![$JIS関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/d5b2d9e417ea41738555b05b6f4333b0.png)

### 計算結果

![$JIS関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/73d633bd9469476ca0db9863db7b1530.png)

## 使用例②

パラメータにチェック項目を指定

### 計算式

![$JIS関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/92eec331e19a49d1822c25a1fba8a43d.png)

### パラメータ

![$JIS関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/3a23f32683ee4cbf97caa941567fb7fa.png)

### 計算結果

![$JIS関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/9a00a8326c23417f91d37ea02179f25c.png)