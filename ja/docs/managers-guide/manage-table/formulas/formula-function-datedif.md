---
title: $DATEDIF関数
category: 計算式
order: '1020'
status: ''
parts: ''
urlstring: formula-function-datedif
translationKey: formula-function-datedif
shortname: $DATEDIF関数
created: 2023-12-06
updated: 2025-07-08
---

## 概要

2つの日付の間の日数、月数、または年数を計算します。

## 構文

```
$DATEDIF(開始日,終了日,計算単位)
```

## パラメータ

|パラメータ|型|必須|説明|
|:--|:--|:--|:--|
|開始日|`yyyy/mm/dd` または `yyyy/mm/dd hh:mm:ss` 形式の日付・時刻、またはそれに準じた日付文字列|必須|開始日＞終了日の場合エラー。|
|終了日|`yyyy/mm/dd` または `yyyy/mm/dd hh:mm:ss` 形式の日付・時刻、またはそれに準じた日付文字列|必須|開始日＞終了日の場合エラー。|
|計算単位|'Y'：年数<br>'M'：月数<br>'D'：日数<br>'H'：時数<br>'N'：分数<br>'S'：秒数<br>'MD'：開始日から終了日までの日数。 日付の月数および年数は無視<br>'YM'：開始日から終了日までの月数。 日付の日数および年数は無視<br>'YD'：開始日から終了日までの日数。 日付の年数は無視|必須||

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|開始日|〇|×|〇|〇|×|
|終了日|〇|×|〇|〇|×|
|計算単位|〇|×|×|〇|×|

## 戻り値

計算単位で指定した数（年数／月数／日数／時数／分数／秒数）。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示|
|数値（作業量、進捗率、残作業量含む）|戻り値を表示|
|日付（開始、完了含む ）|表示しない|
|説明（内容含む）|戻り値を表示|
|チェック（ロック含む）|表示しない|

## 使用例①

パラメータを画面項目名（表示名）で指定。計算単位は「Y」

### 計算式

![$DATEDIF関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6aad51c9efe941569122562714db315e.png)

### パラメータ

![$DATEDIF関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/dc2aed3d8e6e47f181f45a903d320b41.png)

### 計算結果

![$DATEDIF関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/d99fcd8061414253a549ca46658e2c19.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.18.0以降|パラメータ 「時間単位」に 'H'、'N'、'S' を追加|
