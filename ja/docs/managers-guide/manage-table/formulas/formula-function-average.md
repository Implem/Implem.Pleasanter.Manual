---
title: $AVERAGE関数
category: 計算式
order: '1420'
status: ''
parts: ''
urlstring: formula-function-average
translationKey: formula-function-average
shortname: $AVERAGE関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

引数の平均（算術平均）を求めます。

## 構文

```
$AVERAGE(数値1, [数値2],...)  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|数値1|半角数値|必須|平均を求める1つ目の数値。|
|[数値2],...|半角数値|任意|平均を求める追加する数値。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|数値1|〇|〇|×|〇|×|
|[数値2]|〇|〇|×|〇|×|

## 戻り値

引数の平均（算術平均）。
引数にエラー値または数値に変換できない文字列を指定すると、エラーになります。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。値付きドロップダウンリストの場合は値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値を表示。|
|日付（開始、完了含む ）|表示しない。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$AVERAGE関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/67eca952dfbc4821835036b1e962b061.png)

### パラメータ

![$AVERAGE関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/68030f4261ed4f0c9619e57f2f3d4a67.png)

### 計算結果

![$AVERAGE関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/d5532e186891485aa8017b56d7bdef56.png)