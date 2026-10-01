---
title: 書式
category: エディタ
order: '6300'
status: ''
parts: ''
urlstring: table-management-format
translationKey: table-management-format
shortname: 書式
created: 2021-05-03
updated: 2025-06-25
---

## 概要

[数値項目](../../columns/table-management-num.md)の表示フォーマットを指定します。カスタムを指定した場合にはカスタム書式の文字列を指定します。

## 制限事項

1.  [数値項目](../../columns/table-management-num.md)のみ使用できます。
1.  [エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)や[一覧編集](../../../../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)では[カスタム](../../../../../../users-guide/dashboard/dashboard-custom.md)で指定したフォーマットが適用されません。[読取専用](table-management-readonly.md)をオンにした場合には適用されます。
1.  [言語](../../../../../../FAQ/system-requirements-and-setup/faq-supported-language.md)を「Japanese」以外に指定したユーザが利用する場合には「通貨」を使用しないでください。[数値項目](../../columns/table-management-num.md)の[入力検証](../input-validation/index.md)が正しく動作しない問題や、通貨記号が「¥」以外の記号で表示される問題があります。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 設定内容

| No  | 選択肢   | 説明                                                                                                                                                                          |
| :-- | :------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | 標準     | 「123456」のように数値のみで表示します。                                                                                                                                      |
| 2   | 通貨     | 「¥123,456」のように通貨記号および桁区切りを含むフォーマットで表示します。                                                                                                      |
| 3   | 桁区切り | 「123,456」のように桁区切りで表示します。                                                                                                                                     |
| 4   | カスタム | 「[C#のToString関数](https://docs.microsoft.com/ja-jp/dotnet/standard/base-types/standard-numeric-format-strings)」のformat引数にカスタムで指定したフォーマットで表示します。 |

## 関連情報

-   [テーブルの管理：項目：数値](../../columns/table-management-num.md)
-   [テーブル機能：レコードのエディタ画面](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブル機能：レコードの一覧編集](../../../../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)
-   [ダッシュボード機能：パーツの追加：カスタム](../../../../../../users-guide/dashboard/dashboard-custom.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](table-management-readonly.md)
-   [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../../../../FAQ/system-requirements-and-setup/faq-supported-language.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力検証](../input-validation/index.md)
-   [C#のToString関数](https://docs.microsoft.com/ja-jp/dotnet/standard/base-types/standard-numeric-format-strings)
