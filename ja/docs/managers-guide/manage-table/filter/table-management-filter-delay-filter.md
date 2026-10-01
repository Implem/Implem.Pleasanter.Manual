---
title: 遅延フィルタを使用する
category: フィルタ
order: '1100'
status: ''
parts: ''
urlstring: table-management-filter-delay-filter
translationKey: table-management-filter-delay-filter
shortname: 遅延フィルタを使用する
created: 2022-06-16
updated: 2025-01-30
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)で状況が完了以外で、遅延と判断されたレコードを検索します。スケジュール消化率に比べて進捗状況が低いレコードが遅延として扱われます。期限付きテーブルで設定することができます。遅延の条件は以下のとおりです。  

  1. 未完了(状況項目で設定した番号が900未満)
  1. 現在の時刻が完了の日時を過ぎた場合に、進捗率が100%未満の場合  
  1. 進捗状況がスケジュール消化率を満たしていない場合  
  進捗状況 = (現在時刻 - 開始項目※) / (完了項目 - 開始項目※) × 100  
  ※開始項目が未入力の場合は、レコード作成日時になります。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 設定方法

1. テーブルの管理からフィルタタブを選択し、下図のように「遅延フィルタを使用する」にチェックをオンに設定すると一覧画面のフィルタに表示されます。またチェックをオフに設定すると一覧画面でのフィルタに表示されなくなります。

![テーブルの管理のフィルタタブにある「遅延フィルタを使用する」のチェック](https://pleasanter.org/files/images/ja/managers-guide/manage-table/filter/assets/d429dd9c9f7c4cfc8c924f0f7a465ab9.png)

## 動作イメージ

オンの場合
![オンのとき、一覧画面のフィルタに「遅延」が表示された状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/filter/assets/42005e383a424c7683592f034f264ad3.png)

オフの場合
![オフのとき、一覧画面のフィルタに「遅延」が表示されない状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/filter/assets/a0446981f0e54813832691d6488104c3.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.5.0以降|機能追加|

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)