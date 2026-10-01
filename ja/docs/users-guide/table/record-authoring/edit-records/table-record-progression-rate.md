---
title: レコードの進捗率表示
category: テーブル機能
order: '0'
status: ''
parts: ''
urlstring: table-record-progression-rate
translationKey: table-record-progression-rate
shortname: 進捗率
created: 2026-03-25
updated: 2026-08-17
---

## 概要

レコードの「[一覧画面](../data-analysis/table-grid.md)」の「進捗率」では、以下の情報が表示されます。

![一覧画面の進捗率に表示される進捗率・予定帯グラフ・実績帯グラフ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/21df71eb0f50481998862c15a2293660.png)

ユーザが入力した「進捗率」（パーセント値）と、その他の情報から自動生成される帯グラフを用いると、日付ベースの予実確認を行えます。

#### <span class="pl-callout">➊</span>進捗率

ユーザが「[進捗率項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-progress-rate.md)」へ入力した数値（パーセント値）を表示します。

#### <span class="pl-callout">➋</span>予定帯グラフ

「開始」から「完了」までの期間に対する、「開始」から現在の日付までの期間の割合を示す帯グラフです。

1. 予定帯グラフは常に表示します。
1. 「開始」から「完了」までの期間は、薄いグレーの帯で表示します。
1. 「開始」から現在の日付までの期間は、濃いグレーの帯で表示します。
1. 「開始」が未設定の場合は、「作成日時」で表示します。

![開始から現在までの期間を濃いグレーで示した予定帯グラフ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/3e5e8f59b3654a809f28bcea6c11d67b.png)

#### <span class="pl-callout">➌</span>実績帯グラフ

現在の進捗率を示す帯グラフです。

1. 実績帯グラフはユーザが「進捗率」を設定すると表示します。
1. 日付経過と比べ進捗が「進んでいる」場合、グリーンの帯で表示します。
1. 日付経過と比べ進捗が「遅れている」場合、レッドの帯で表示します。

![現在の進捗率を示す実績帯グラフ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/fd9fa979cb14443cbdad9ae366c4428b.png)

## 進捗率表示のカスタマイズ

進捗率表示のカスタマイズについては、以下のFAQを確認してください。

1. [FAQ：状況項目の値により進捗率を自動で指定する](../../../../FAQ/editor/faq-automatic-entry-of-progress-rate.md)
1. [FAQ：一覧画面の進捗率に表示されるグラフを非表示にしたい](../../../../FAQ/editor/hide-progress-graph-on-grid.md)

## 制限事項

1. 「[進捗率項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-progress-rate.md)」は「記録テーブル」では使用できません。
