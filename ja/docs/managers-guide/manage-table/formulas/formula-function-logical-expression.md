---
title: 計算式（拡張）の関数で使用する論理式
category: 計算式
order: '40'
status: ''
parts: ''
urlstring: formula-function-logical-expression
translationKey: formula-function-logical-expression
shortname: 計算式（拡張）の場合分け計算
created: 2023-12-06
updated: 2026-02-10
---

## 概要

[計算式（拡張）](table-management-formula-extended.md)の関数で使用する論理式について説明します。論理式は[$IF関数](formula-function-if.md)などの条件判定で利用します。

## 1. 論理関数を使用する

[$AND関数](formula-function-and.md)、[$OR関数](formula-function-or.md)などの論理関数を使用します。

### 論理関数の使用例

-   チェックA、チェックBのどちらか一方がオンの場合、分類Aに"チェック済み"と表示します。  
-   チェックA、チェックBのどちらもオフの場合、"未チェック"と表示します。

![論理関数を使った計算式の設定例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/aa276622415f45a7a95b3845770daf06.png)

```js
$IF($OR(チェックA,チェックB),"チェック済み","未チェック")
```

## 2. JavaScriptの比較演算子を使用する

[計算式（拡張）](table-management-formula-extended.md)では、以下のJavaScriptの比較演算子を使用できます。

|演算子|説明|trueを返す例|
|:---|:---|:---|
|==（等しい）|左辺と右辺が等しい場合にtrueを返します|分類A == "中野区"|
|!=（等しくない）|左辺と右辺が等しくない場合にtrueを返します|分類A != "中野区"|
|>（大なり）|左辺が右辺より大きい場合にtrueを返します|数値A > 1000|
|>=（以上）|左辺が右辺以上の場合にtrueを返します|数値A >= 1000|
|<（小なり）|左辺が右辺より小さい場合にtrueを返します|数値A < 1000|
|<=（以下）|左辺が右辺以下の場合にtrueを返します|数値A <= 1000|

### JavaScriptの比較演算子の使用例

-   会計が1000円を超える場合は、定価の10%割引額を、会計（キャンペーン）に表示します。
-   会計が1000円以下の場合は、定価を会計（キャンペーン）に表示します。

![JavaScriptの比較演算子を使った計算式の設定例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/065bc32f27b54c69a0f7ff55e57b262e.png)

```js
$IF(会計 > 1000, 価格 * 注文数 * 0.9, 価格 * 注文数)
```

## 関連情報

-   [テーブルの管理：計算式（拡張）](table-management-formula-extended.md)
-   [$IF関数](formula-function-if.md)
-   [$AND関数](formula-function-and.md)
-   [$OR関数](formula-function-or.md)