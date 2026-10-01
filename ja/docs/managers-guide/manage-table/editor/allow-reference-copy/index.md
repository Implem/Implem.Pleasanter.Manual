---
title: 参照コピーを許可
category: エディタ
order: '23420'
status: ''
parts: ''
urlstring: table-management-allow-reference-copy
translationKey: table-management-allow-reference-copy
shortname: 参照コピーを許可,参照コピー
created: 2021-09-26
updated: 2025-01-30
---

## 概要

レコードの[参照コピー](../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)を許可します。[参照コピー](../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)を許可する場合にはオンに設定します。[参照コピー](../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)が許可されていない場合、[エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)の参照コピーボタンが非表示となります。参照コピーを行うと、新規作成前の状態でデータがコピーされ、必要な情報を変更した後にレコードを作成することができます。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 既定値

既定値はオフです。[General.json](../../../../setup/parameters/general.json.md)の「AllowReferenceCopy」で変更可能です。

## 操作手順

1.  対象の[テーブル](../../../../users-guide/table/index.md)を開いてください。
1.  「管理」メニューから[テーブルの管理](../../index.md)をクリックしてください。
1.  [エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを開いてください。
1.  画面下部にある「参照コピーを許可」のチェックボックスをオンまたはオフにしてください。
1.  画面下部の「更新」ボタンをクリックしてください。

## 動作イメージ

参照コピーを許可すると、参照コピーボタンが表示されます。

![参照コピーボタンが表示されたレコードの編集画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/allow-reference-copy/assets/f334f9b77daa4e2d9759f640e94c6b42.png)

参照コピーを実施すると、新規作成画面へ遷移します。この時点でレコードは作成されません。

![参照コピーで開いた新規作成画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/allow-reference-copy/assets/5d747857c53547928c58dc9150d9145b.png)

必要な情報を入力し、レコードを作成してください。

## 関連情報

-   [応用編：コピーと参照コピー](../../../../users-guide/hands-on/advanced/advanced-operations-copy.md)
-   [テーブル機能：レコードのエディタ画面](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [パラメータ設定：General.json](../../../../setup/parameters/general.json.md)
-   [テーブル機能](../../../../users-guide/table/index.md)
-   [テーブルの管理](../../index.md)
