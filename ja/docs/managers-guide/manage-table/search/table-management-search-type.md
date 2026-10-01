---
title: 検索の種類
category: 検索
order: '1000'
status: ''
parts: ''
urlstring: table-management-search-type
translationKey: table-management-search-type
shortname: 検索の種類,検索：検索の種類
created: 2021-05-30
updated: 2023-05-18
---

## 概要

キーワードによる[検索](index.md)を行う際の検索方法を指定します。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 設定内容

| No  | 項目名             | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :-- | :----------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | フルテキスト       | [フルテキストデータ](fulltext-settings/index.md)に記録された文字列をデータベースのフルテキスト検索機能を使用して検索します。大量のレコードが保存されていても、高速に検索可能です。データベースの機能により自動的に単語の分かち書きが行われるため、単語によってはヒットしない場合があります。（例：「東京都」 → [東][京都] or [東京都] として登録されるため、[東][京都]として登録されてしまった場合は「東京都」で検索してもヒットしない） |
| 2   | 部分一致           | [フルテキストデータ](fulltext-settings/index.md)に記録された文字列の部分一致検索を行います。フルテキストと比べるとユーザの意図通りの検索結果を得ることができます。大量のレコードが登録されている場合、検索に時間がかかる場合があります。                                                                                                                                                                                               |
| 3   | タイトルの前方一致 | [タイトル項目](../editor/editor-settings/columns/table-management-title.md)に記録された文字列を前方一致検索で検索します。アルファベットの大文字/小文字は区別しません。[タイトル結合](../editor/editor-settings/advanced-settings/general/table-management-title-combination.md)を行っている場合には結合後のタイトルを対象に検索します。                                                                                                             |
| 4   | タイトルの部分一致 | [タイトル項目](../editor/editor-settings/columns/table-management-title.md)に記録された文字列を部分一致検索で検索します。アルファベットの大文字/小文字は区別しません。[タイトル結合](../editor/editor-settings/advanced-settings/general/table-management-title-combination.md)を行っている場合には結合後のタイトルを対象に検索します。                                                                                                             |

## 関連情報

-   [テーブルの管理：検索](index.md)
-   [テーブルの管理：検索：フルテキストの設定](fulltext-settings/index.md)
-   [テーブルの管理：項目：タイトル](../editor/editor-settings/columns/table-management-title.md)
-   [テーブルの管理：エディタ：項目の詳細設定：タイトル結合](../editor/editor-settings/advanced-settings/general/table-management-title-combination.md)
