---
title: $WEEKDAY関数
category: 計算式
order: '1110'
status: ''
parts: ''
urlstring: formula-function-weekday
translationKey: formula-function-weekday
shortname: $WEEKDAY関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

日付に対応する曜日を求めます。

## 構文

```
$WEEKDAY(日付,[週の基準])
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|日付|yyyy/mm/dd形式の日付または日付文字列|必須||
|[週の基準]|1～3および11～17の半角数値|任意|設定した値に応じて戻り値の範囲を決定する。省略時は1が設定されたとみなす。<br>1：1（日曜）～7（土曜）の範囲の整数を返す<br>2：1（月曜）～7（日曜）の範囲の整数を返す<br>3：0（月曜）～6（日曜）の範囲の整数を返す<br>11：1（月曜）～7（日曜）の範囲の整数を返す<br>12：1（火曜）～7（月曜）の範囲の整数を返す<br>13：1（水曜）～7（火曜）の範囲の整数を返す<br>14：1（木曜）～7（水曜）の範囲の整数を返す<br>15：1（金曜）～7（木曜）の範囲の整数を返す<br>16：1（土曜）～7（金曜）の範囲の整数を返す<br>17：1（日曜）～7（土曜）の範囲の整数を返す|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|日付|〇|×|〇|〇|×|
|[週の基準]|〇|〇|×|〇|×|

## 戻り値

1～7、または0～6の範囲の整数。

### 戻り値の表示内容

|対象|戻り値の表示内容|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示|
|数値（作業量、進捗率、残作業量含む）|戻り値を表示|
|日付（開始、完了含む ）|表示しない|
|説明（内容含む）|戻り値を表示|
|チェック（ロック含む）|表示しない|

## 使用例①

パラメータを画面項目名（表示名）で指定。

### 計算式

![$WEEKDAY関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/58540cf6e08242d4a483a04284fba861.png)

### パラメータ

![$WEEKDAY関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/24eb3a668a76420c8a37caf901adcd67.png)

### 計算結果

![$WEEKDAY関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/230ecb54c1824661a5e83fa85cc632b5.png)

## 使用例②

パラメータを画面項目名（表示名）で指定。パラメータ[週の基準]も指定。

### 計算式

![$WEEKDAY関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/464af93b4ee14d059b8b2ca403639989.png)

### パラメータ

![$WEEKDAY関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/80fbe96062064fbcaab11b874798e56c.png)

### 計算結果

![$WEEKDAY関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/54169a6ad4d64e8d823c4695a80d415b.png)

