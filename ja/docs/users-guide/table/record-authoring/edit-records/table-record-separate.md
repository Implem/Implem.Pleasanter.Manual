---
title: レコードの分割
category: テーブル機能
order: '711'
status: ''
parts: ''
urlstring: table-record-separate
translationKey: table-record-separate
shortname: 分割
created: 2019-04-29
updated: 2023-10-13
---

## 概要

期限付きテーブルに登録した1つのレコードを複数のレコードに分割するための機能です。分割する際にはタイトルの編集と作業量の割り振りを行うことができます。分割元になったレコードのコメント欄には、各レコードへのリンクが自動的に挿入されます。分割元のレコードのIDは変更されません。分割先のレコードは新規に作成されます。

## 制限事項

1. [テーブルの管理](../../../../managers-guide/manage-table/index.md)の[分割を許可](../../../../managers-guide/manage-table/editor/allow-separating-record/index.md)がオフの場合、「分割」ボタンが非表示となり操作が行えません。
1. [添付ファイル](table-record-attachment-delete.md)は分割先のレコードにコピーできません。
1. 「閲覧履歴」は分割先のレコードにコピーできません。
1. [レコードのアクセス制御](../../../access-control/table-record-access-control.md)の設定は分割先のレコードにコピーできません。
1. 分割数の上限は 10 です。上限は[General.json](../../../../setup/parameters/general.json.md)の「SeparateMax」で指定します。

## 前提条件

1. 「読み取り権限」と「更新権限」が必要です。
1. 期限付きテーブルに登録したレコードが分割可能です。

## 操作手順

1. 対象のテーブルに移動してください。
1. [一覧画面](../data-analysis/table-grid.md)から対象のレコードを検索してください。
1. 対象のレコードをクリックしてください。
1. 画面下の「分割」ボタンをクリックしてください。
1. 分割数にいくつに分割するか入力してください。
1. 分割後のタイトルを変更したい場合は、タイトルを修正してください。また、分割元のレコードからどの程度作業量を振り分けるか入力してください。
1. 「分割」ボタンをクリックしてください。「分割してもよろしいですか」とポップアップが表示されますので、OKをクリックしてください。
1. 画面下に「分割しました。」とメッセージが表示されたら完了です。

## 関連情報

-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)
-   [テーブルの管理：エディタ：分割を許可](../../../../managers-guide/manage-table/editor/allow-separating-record/index.md)
-   [テーブル機能：レコードの添付ファイルの削除](table-record-attachment-delete.md)
-   [レコードのアクセス制御（レコードの編集）](../../../access-control/table-record-access-control.md)
-   [テーブル機能：レコードの一覧画面](../data-analysis/table-grid.md)