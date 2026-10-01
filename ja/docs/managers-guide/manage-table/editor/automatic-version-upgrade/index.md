---
title: 自動バージョンアップ
category: エディタ
order: '23000'
status: ''
parts: ''
urlstring: table-management-auto-version-up
translationKey: table-management-auto-version-up
shortname: 自動バージョンアップ,新バージョンとして保存
created: 2021-05-01
updated: 2024-04-09
---

## 概要

自動バージョンアップの種類を設定します。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 操作手順

1.  対象の[テーブル](../../../../users-guide/table/index.md)を開いてください。
1.  「管理」メニューから[テーブルの管理](../../index.md)をクリックしてください。
1.  [エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを開いてください。
1.  画面下部にある「自動バージョンアップ」のセレクトボックスから任意の設定を選択してください。
1.  画面下部の「更新」ボタンをクリックしてください。

## 設定内容

| 選択肢 | 説明                                                                                               |
| :----- | :------------------------------------------------------------------------------------------------- |
| 既定   | 更新日、更新者が異なる場合に新バージョンとして保存する。                                           |
| 常時   | 更新日、更新者が同一でも新バージョンとして保存する（「新バージョンとして保存」は変更できません）。 |
| 無効   | 更新日、更新者が異なる場合でも新バージョンとして保存しない。                                       |

## 動作イメージ

データを更新する際のバージョン管理方法を設定します。

![エディタタブの「自動バージョンアップ」の設定欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/automatic-version-upgrade/assets/faaef3f8958d4b459a646a68fd5397a9.png)

[エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)においては画面下部に表示される「新バージョンとして保存」のチェックボックスの初期値の指定となります。「既定」の場合、レコードの最新バージョンと比較して更新日または更新者のどちらかが異なる場合は[エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)を開くとチェックされた状態になります。

## 関連情報

-   [テーブル機能](../../../../users-guide/table/index.md)
-   [テーブルの管理](../../index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
