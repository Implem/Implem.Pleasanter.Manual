---
title: $SEARCH関数
category: 計算式
order: '1230'
status: ''
parts: ''
urlstring: formula-function-search
translationKey: formula-function-search
shortname: $SEARCH関数
created: 2023-12-06
updated: 2024-06-07
---

## 概要

検索文字列を対象の文字列の中で検索し、検索文字列が最初に現れる位置を左端から数えた結果を求めます。検索は大文字小文字は区別されません。ワイルドカード文字は使用できません。

## 構文

```
$SEARCH(検索文字列,対象の文字列,[開始位置])
```

## パラメータ

|パラメータ|型|必須|説明|
|:---|:---|:---|:---|
|検索文字列|任意の文字列|必須||
|対象の文字列|任意の文字列|必須||
|開始位置|半角数値。1以上の整数|任意|検索を開始する位置を指定。「対象の文字列」の先頭文字から検索を行う場合は1を指定。省略時は1を指定したとみなす。|

### パラメータに利用可能な項目

|パラメータ|分類|数値|日付|説明|チェック|
|:---|:---|:---|:---|:---|:---|
|検索文字列|〇|〇|〇|〇|×|
|対象の文字列|〇|〇|〇|〇|×|
|[開始位置]|〇|〇|×|〇|×|

## 戻り値

検索文字列が最初に現れた位置（1以上の整数）。
検索文字列が見つからなかった場合はエラーとなります。
開始位置が対象の文字列の文字数より大きい場合はエラーとなります。

### 対象とする項目に対する戻り値

|対象|戻り値|
|:---|:---|
|分類（タイトル、状況、管理者、担当者含む）|戻り値を表示。値付きドロップダウンリストの場合は戻り値に合致した選択肢を表示。|
|数値（作業量、進捗率、残作業量含む）|戻り値を表示。|
|日付（開始、完了含む ）|表示しない。|
|説明（内容含む）|戻り値を表示。|
|チェック（ロック含む）|表示しない。|

## 使用例①

パラメータを画面項目名（表示名）で指定
![$SEARCH関数を使った使用例①の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/ba5afaa308f0489789bc231db5ba48e4.png)

### パラメータ

![$SEARCH関数の使用例①で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/762191cb9efa46d69da39ce8083332aa.png)

### 計算結果

![$SEARCH関数の使用例①の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/9720579d3044440abcafe5eb9fd3a244.png)

## 使用例②

パラメータ[開始位置]を指定

### 計算式

![$SEARCH関数を使った使用例②の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a2a5e5ecda374db989a50f9417a0025d.png)

### パラメータ

![$SEARCH関数の使用例②で指定したパラメータ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6a39ab18c51e4f0d97b9b54b242733af.png)

### 計算結果

![$SEARCH関数の使用例②の計算結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/0767692bfb0143b0a15b02fd547a990d.png)