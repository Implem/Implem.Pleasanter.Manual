---
title: 端数処理種類
category: エディタ
order: '6700'
status: ''
parts: ''
urlstring: table-management-rounding-type
translationKey: table-management-rounding-type
shortname: 端数処理種類
created: 2021-05-03
updated: 2024-04-09
---

## 概要

[数値項目](../../columns/table-management-num.md)の小数点以下の端数処理の種別を指定します。[小数点以下桁数](table-management-decimal-places.md)で指定した桁数で数値の丸めを行います。

## 制限事項

1.  [数値項目](../../columns/table-management-num.md)でのみ設定できます。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 設定内容

![数値項目の詳細設定の「端数処理種類」の選択欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/c1d0c6f124a747c29808a3e4ceda0e38.png)

| No  | 選択肢       | 説明                                                                                                                                                  |
| :-- | :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | 四捨五入     | 端数が0から4ならばゼロ方向に丸める。5から9ならばゼロとは反対方向に丸める。                                                                            |
| 2   | 切り上げ     | 端数を正の方向に丸める。                                                                                                                              |
| 3   | 切り下げ     | 端数を負の方向に丸める。                                                                                                                              |
| 4   | 切り捨て     | 端数をゼロ方向に丸める。                                                                                                                              |
| 5   | 銀行家の丸め | 端数の数値が0.5より小さいなら切り捨て、端数が0.5より大きいならば切り上げる。端数がちょうど0.5なら切り捨てと切り上げのうち結果が偶数となる方へ丸める。 |

## 関連情報

-   [テーブルの管理：項目：数値](../../columns/table-management-num.md)
-   [テーブルの管理：エディタ：項目の詳細設定：小数点以下桁数](table-management-decimal-places.md)
