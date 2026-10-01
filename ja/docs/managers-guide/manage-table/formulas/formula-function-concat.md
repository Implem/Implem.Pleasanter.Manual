---
title: $CONCAT関数
category: 計算式
order: '1140'
status: ''
parts: ''
urlstring: formula-function-concat
translationKey: formula-function-concat
shortname: $CONCAT関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

指定した文字列を結合します。

## 構文

```
$CONCAT(テキスト1,[テキスト2],...)
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|テキスト1|任意の文字列|必須||
|[テキスト2],...|任意の文字列|任意||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|テキスト1|〇|〇|〇※1|〇|〇※2|
|[テキスト2],...|〇|〇|〇※1|〇|〇※2|

※1：[エディタの書式](../editor/editor-settings/advanced-settings/general/table-management-editor-format.md)で指定した書式を出力します。
※2：”true”または”false”という文字列を出力します。

## 戻り値

結合した文字列。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。戻り値が半角数値の場合でかつ値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示|
|数値（作業量、進捗率、残作業量含む）|戻り値が半角数値の場合に限り戻り値を表示。|
|日付（開始、完了含む ）|戻り値が日付形式の場合に限り戻り値を表示。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$CONCAT関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/1ca9f8aad77746c59d428e751904b274.png)

### パラメータ

![$CONCAT関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/0975ed9ec0164376a0df38953e560c21.png)

### 計算結果

![$CONCAT関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/0a307ce94eaf4e86a1f7cae57127b6fb.png)

## 使用例②

パラメータを4つ指定。

### 計算式

![$CONCAT関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/86c7a189660643d9be795a819b06af78.png)

### パラメータ

![$CONCAT関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/235498db337846c894e7e4d337813745.png)

### 計算結果

![$CONCAT関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/38d35ce25b2843c0824def3caa8977ad.png)
