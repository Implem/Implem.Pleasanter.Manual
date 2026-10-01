---
title: レコードの削除
category: テーブル機能
order: '601'
status: ''
parts: ''
urlstring: table-record-delete
translationKey: table-record-delete
shortname: レコードの削除,削除
created: 2021-04-17
updated: 2024-06-07
---

## 概要

[エディタ](table-editor.md)を使用して、テーブルのレコードを削除します。この操作を行うとレコードは[ごみ箱](table-record-physical-delete.md)に移動します。

## 制限事項

1. [テーブル](../../index.md)がロックされている場合には削除できません。
1. レコードがロックされている場合には削除できません。
1. 読取専用となっている場合は削除できません。
1. レコードを削除してもレコードに登録した画像は削除されません。

## 前提条件

1. [サイト](../../../site/index.md)またはレコードに「読み取り権限」と「削除権限」が必要です。

## 操作手順

1. 対象のテーブルに移動してください。
1. [一覧画面](../data-analysis/table-grid.md)から対象のレコードを検索してください。
1. 対象のレコードをクリックしてください。
1. [エディタ](table-editor.md)が表示されますので、削除してよいか確認してください。
1. 「削除」ボタンをクリックしてください。
1. 確認ダイアログが表示されるので「OK」をクリックしてください。
1. 「"xxxx"を削除しました。」と表示されれば完了です。xxxxにはレコードのタイトルが表示されます。

![エディタの「削除」ボタンからレコードを削除する操作の画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/21ec606ebf5040f4997717877a84035b.png)

## 関連情報

-   [テーブル機能：レコードのエディタ画面](table-editor.md)
-   [テーブル機能：レコードをごみ箱から削除](table-record-physical-delete.md)
-   [テーブル機能](../../index.md)
-   [サイト機能](../../../site/index.md)
-   [テーブル機能：レコードの一覧画面](../data-analysis/table-grid.md)