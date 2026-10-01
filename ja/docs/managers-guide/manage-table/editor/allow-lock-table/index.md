---
title: テーブルのロックを許可
category: エディタ
order: '23700'
status: ''
parts: ''
urlstring: table-management-table-lock
translationKey: table-management-table-lock
shortname: テーブルのロック,テーブルのロックを許可
created: 2021-05-01
updated: 2024-04-09
---

## 概要

「テーブルのロック」を許可します。「レコード」単位のロックを許可する場合には[レコードのロックを許可](../editor-settings/advanced-settings/general/table-management-record-lock.md)を参照してください。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 操作手順

1.  対象の[テーブル](../../../../users-guide/table/index.md)を開いてください。
1.  「管理」メニューから[テーブルの管理](../../index.md)をクリックしてください。
1.  [エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを開いてください。
1.  画面下部にある「テーブルのロックを許可」のチェックボックスをオンにしてください。
1.  画面下部の「更新」ボタンをクリックしてください。

## 動作イメージ

「テーブルのロックを許可」にチェックをいれていない場合の「管理」メニュー(許可していない場合 ※標準設定)

![「テーブルのロックを許可」がオフのときの「管理」メニュー](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/allow-lock-table/assets/a1070bdae81a485ab85be138dfb3b92d.png)

「テーブルのロックを許可」にチェックをいれている場合の「管理」メニュー(許可している場合)

![「テーブルのロックを許可」がオンのときの「管理」メニュー](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/allow-lock-table/assets/93fda281b4cb4a61af34a12834608390.png)

テーブルをロックしている場合の一覧画面

![テーブルをロックしている状態の一覧画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/allow-lock-table/assets/66e101487bd145fab56045e47104eee2.png)

テーブルをロックしている場合の編集画面

![テーブルをロックしている状態の編集画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/allow-lock-table/assets/38282f8ac1294e39a4ca943db7298c21.png)

**ロック状態を解除できるのはテーブルをロックしたユーザ、または[特権ユーザ](../../../user-administration/user-management-privileged-users.md)が「テーブルのロックを解除」する必要があります。**

## 関連情報

-   [テーブルの管理：エディタ：レコードのロックを許可](../editor-settings/advanced-settings/general/table-management-record-lock.md)
-   [テーブル機能](../../../../users-guide/table/index.md)
-   [テーブルの管理](../../index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [ユーザ管理機能：特権ユーザの設定](../../../user-administration/user-management-privileged-users.md)
