---
title: ビューのリセットを許可
category: 一覧画面
order: '252'
status: ''
parts: ''
urlstring: table-management-permission-view-reset
translationKey: table-management-permission-view-reset
shortname: ビューのリセットを許可
created: 2021-10-19
updated: 2024-05-24
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)の「ビューのリセットを許可」を設定します。ビューのリセットを許可させない設定をすると、初期状態のビューが選択できなくなります。

「ビューのリセットを許可」する → 初期状態のビューが選択できる
![「ビューのリセットを許可」したとき、初期状態のビューを選べる状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/a677eada9d5d4d55ab209226812a7f0e.png)

「ビューのリセットを許可」しない → 初期状態のビューが選択できない
![許可しないとき、初期状態のビューを選べない状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/00f696015a9349a48e86e4a3738abab7.png)

例えば、一覧画面で特定のコマンドボタンを非表示とするビューを用意した場合、初期状態のビューにリセットすると、非表示としたボタンが再表示されてしまいます。  ビューのリセットを許可しない設定とすることで、特定のボタンを利用させなくする等の制御が可能となります。

## 制限事項

1. [テーブルの管理](../index.md)の[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)を事前に設定した上で利用します。ビューが設定されていないと、正しく機能を利用することができません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。
1. [ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)が1つ以上作成されていることが必要です。

ビューを設定済みの場合のみ「ビューのリセットを許可」の選択肢が表示されます。
![ビューを設定済みのとき、一覧タブに「ビューのリセットを許可」が出た状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/595b2d1bd9bc42c1a611a24800e39f77.png)
ビューを設定していない場合「ビューのリセットを許可」は表示されません。  
![ビューを設定していないとき、一覧タブに「ビューのリセットを許可」が出ない状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/61fe004d0a40416d9d69a791746d4e35.png)

## 操作手順

1. 対象の[テーブル](../../../users-guide/table/index.md)を開いてください。
1. 「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1. [一覧](index.md)タブを開いてください。
1. 画面下部にある「ビューのリセットを許可」のチェックボックスを設定してください。
1. 画面下部の「更新」ボタンをクリックしてください。

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理](../index.md)
-   [応用編：ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [テーブルの管理：一覧画面](index.md)