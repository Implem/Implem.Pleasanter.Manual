---
title: $SUBSTITUTE関数
category: 計算式
order: '1240'
status: ''
parts: ''
urlstring: formula-function-substitute
translationKey: formula-function-substitute
shortname: $SUBSTITUTE関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

対象の文字列内にある特定の文字列を指定した文字列に変換します。

## 構文

```
$SUBSTITUTE(対象の文字列,検索文字列,置換文字列,[置換対象])  
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|対象の文字列|任意の文字列|必須||
|検索文字列|任意の文字列|必須||
|置換文字列|任意の文字列|必須||
|[置換対象]|半角数値。1以上の整数|任意|対象の文字列に含まれる検索文字列のうち、どの検索文字列を置換するかを指定。「2」と指定した場合、2番目に現れる検索文字列のみを置換する。省略時は対象の文字列内に現れる検索文字列全てを置換する。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|対象の文字列|〇|〇|〇|〇|×|
|検索文字列|〇|〇|〇|〇|×|
|置換文字列|〇|〇|〇|〇|×|
|置換対象|〇|〇|×|〇|×|

## 戻り値

置換後の文字列。

### 対象とする項目に対する戻り値

|対象|戻り値|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。戻り値が半角数値の場合でかつ値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値が半角数値の場合に限り戻り値を表示。|
|日付（開始、完了含む ）|戻り値が日付形式の文字列の場合に限り戻り値を表示。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定

### 計算式

![$SUBSTITUTE関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/887a11e0035b40768d0999ebc4a19c1a.png)

### パラメータ

![$SUBSTITUTE関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/016cf29e271f4f93adbc436fa6b8568c.png)

### 計算結果

![$SUBSTITUTE関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/f1ec15d6a2a24b599044e82aafec5f46.png)

## 使用例②

パラメータを[置換対象]を指定

### 計算式

![$SUBSTITUTE関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/7286cb533cf54155b923a0b6499fdc9b.png)

### パラメータ

![$SUBSTITUTE関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/11dbe6fd7aa840a59ca3bc19d054668f.png)

### 計算結果

![$SUBSTITUTE関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/296d6db5f02249c199f5e99e256ffd86.png)