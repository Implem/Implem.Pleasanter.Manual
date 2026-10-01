---
title: エディタの書式
category: エディタ
order: '4200'
status: ''
parts: ''
urlstring: table-management-editor-format
translationKey: table-management-editor-format
shortname: エディタの書式
created: 2021-05-05
updated: 2024-12-19
---

## 概要

[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)の[日付項目](../../columns/table-management-date.md)の入力フォーマットに「日付のみ」または「日付と時刻」を設定します。

## 制限事項

1.  [開始項目](../../columns/table-management-start-time.md)、[完了項目](../../columns/table-management-completion-time.md)、[日付項目](../../columns/table-management-date.md)でのみ使用可能です。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 設定内容

| No  | 選択肢         | 説明                           |
| :-- | :------------- | :----------------------------- |
| 1   | 年月日         | 年月日の入力書式です。         |
| 2   | 日付と時刻(分) | 年月日と時分の入力書式です。   |
| 3   | 日付と時刻(秒) | 年月日と時分秒の入力書式です。 |

## 動作イメージ

=== "年月日"

    ![書式が「年月日」の日付項目の入力欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/3f0a32156e784052ac7b48d9b24a6cba.png)

=== "「日付と時刻(分)」および「日付と時刻(秒)」"

    ![書式が「日付と時刻」の日付項目の入力欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/8b1ed1f98f9d4499adeb1e49e3888cb8.png)

    「日付と時刻(秒)」の場合は、項目表示時に秒が表示されます。

## 対応バージョン

| 対応バージョン | 内容                     |
| :------------- | :----------------------- |
| 1.2.16.0以降   | 「日付と時刻(秒)」を追加 |

## 関連情報

-   [テーブル機能：レコードのエディタ画面](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：項目：日付](../../columns/table-management-date.md)
-   [テーブルの管理：項目：開始](../../columns/table-management-start-time.md)
-   [テーブルの管理：項目：完了](../../columns/table-management-completion-time.md)
