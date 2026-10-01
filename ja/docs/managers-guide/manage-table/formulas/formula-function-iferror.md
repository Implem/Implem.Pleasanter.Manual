---
title: $IFERROR関数
category: 計算式
order: '1295'
status: ''
parts: ''
urlstring: formula-function-iferror
translationKey: formula-function-iferror
shortname: $IFERROR関数
created: 2023-12-27
updated: 2024-06-07
---

## 概要

値がエラーの場合に指定した値を返します。エラーでない場合は値を返します。

## 構文

```
$IFERROR(値,エラーの場合の値)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|値|計算式|必須|エラーかどうかをチェックする値、数式、計算式|
|エラーの場合の値|計算式|必須|第一引数「値」がエラーの場合に返す値、数式、計算式|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|値|〇|〇|〇|〇|〇|
|エラーの場合の値|〇|〇|〇|〇|〇|

## 戻り値

値がエラーの場合はエラーの場合の値、そうでない場合は値

### 対象とする項目に対する戻り値

|対象|戻り値|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。戻り値が半角数値の場合でかつ値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示|
|数値（作業量、進捗率、残作業量含む）|戻り値が半角数値の場合に限り戻り値を表示。|
|日付（開始、完了含む ）|戻り値が日付形式の場合に限り戻り値を表示。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|戻り値がtrueの場合チェックON、falseの場合チェックOFF|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$IFERROR関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/7ffe7569e82f47fa8eed75f6482b46f4.png)

### パラメータ

![$IFERROR関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/ba350c7d380143fcb18bf5d4c6b402a2.png)

### 計算結果

![$IFERROR関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c9ce68dd917b46f0ba83a0a0bb859027.png)

## 使用例②

他の関数との組み合わせ

### 計算式

![$IFERROR関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a0cdf75aae74472780739d1dd7d156da.png)

### パラメータ

![$IFERROR関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/08ab89e7d8ae4e91a81aad374876a2fd.png)

### 計算結果

![$IFERROR関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c0c2c4494fe84fcdbc4fbfaa00c929b4.png)
