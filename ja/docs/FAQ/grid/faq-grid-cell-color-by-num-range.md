---
title: 一覧画面で数値の範囲によってセルの色を変えたい
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-grid-cell-color-by-num-range
translationKey: faq-grid-cell-color-by-num-range
shortname: セルCSS
created: 2020-12-15
updated: 2026-02-24
---

## 回答

[サーバスクリプト](../../developers-guide/server-script/index.md)と[スタイル](../../developers-guide/style/index.md)を使用してください。

---

## 概要

[サーバスクリプト](../../developers-guide/server-script/index.md)で[一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)上の指定した[数値項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)の範囲によって「[セルCSS](../../managers-guide/manage-table/grid/advanced-settings/table-management-extended-cell-css.md)」を割り当て、セルの背景色を変更します。

![一覧画面で数値の範囲に応じてセルの背景色が変わっている状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/7bf70f69b9c2414a847c51c5a724c98a.png)

## 操作手順

1. [テーブル](../../users-guide/table/index.md)を作成します。
1. 「数値C(NumC)」を[一覧画面の項目の設定](../../managers-guide/manage-table/grid/table-management-grid-columns.md)で有効化します。  
1. 以下の[サーバスクリプト](../../developers-guide/server-script/index.md)を「新規作成」します。  [条件](../../developers-guide/server-script/basics/server-script-conditions.md)は"行表示の前"を選択します。
1. 以下の[スタイル](../../developers-guide/style/index.md)を「新規作成」します。  「出力先」は"一覧"を選択します。

## スクリプト

##### JavaScript（サーバスクリプト）

```
// 数値Cの値が10,000未満であれば背景を赤、20,000〜30,000未満であれば黄色、30,000以上であれば青に変更します。背景色の指定は、事前に設定したスタイルを使用します。
const total = model.NumC;
if (total < 10000) {
    columns.NumC.ExtendedCellCss = 'cell-blue';
} else if (total >= 10000 && total < 30000) {
    columns.NumC.ExtendedCellCss = 'cell-yellow';
} else if (total >= 30000) {
    columns.NumC.ExtendedCellCss = 'cell-red';
}
```

## スタイル

ver1.4.20.0前後で記載方法が異なりますのでご注意ください。

#### ver1.4.20.0以降

##### CSS（スタイル）

```
/* 合計が10000円未満 */
.grid td.cell-blue {
    background-color: blue;
    color: white;
}
/* 合計が10000円以上、30000円未満 */
.grid td.cell-yellow {
    background-color: yellow;
    color: black;
}
/* 合計が30000円以上 */
.grid td.cell-red {
    background-color: red;
    color: black;
}
```

#### ver1.4.19.2以前

##### CSS（スタイル）

```
/* 合計が10000円未満 */
.cell-blue {
    background-color: blue;
    color: white;
}
/* 合計が10000円以上、30000円未満 */
.cell-yellow {
    background-color: yellow;
    color: black;
}
/* 合計が30000円以上 */
.cell-red {
    background-color: red;
    color: black;
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブル機能：レコードの一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理：項目：数値](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブル機能](../../users-guide/table/index.md)
-   [テーブルの管理：一覧画面：一覧画面の項目の設定](../../managers-guide/manage-table/grid/table-management-grid-columns.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../editor/faq-condition-mode-range.md)