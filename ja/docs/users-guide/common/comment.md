---
title: コメントを追加
category: 共通機能
order: '20'
status: ''
parts: ''
urlstring: comment
translationKey: comment
shortname: コメント
created: 2019-04-30
updated: 2023-05-18
---

## 概要

[エディタ](../table/record-authoring/edit-records/table-editor.md)のコメント欄を使用して「コメント」を登録できます。コメントを追加すると自動的に日時と名前を記録します。コメントは[マークダウン](markdown.md)が使用できます。「コメント」に入力したURLやUNCパスは自動的にハイパーリンクとして表示されます。「コメント」に長文を入力した場合、[一覧画面](../table/record-authoring/data-analysis/table-grid.md)上では先頭のみが表示され、マウスオーバーを行うことで全体を広げて表示します。

## 前提条件

1.  「テナント管理機能」、「組織管理機能」、「ユーザ管理機能」の場合には「テナント管理権限」が必要です。
1.  「グループ管理機能」の場合には「テナント管理権限」または「グループの管理者権限」が必要です。
1.  [サイト機能](../site/index.md)の管理画面の場合には「サイトの管理権限」が必要です。
1.  「テーブル機能」のレコードおよび「Wiki機能」の場合には「更新権限」が必要です。

## コメントの削除

1.  コメントの削除には前提条件に記載した権限が必要です。
1.  削除は自分自身が登録したコメントだけでなく、他ユーザが登録したコメントも削除できます。

## コメントの編集を許可

デフォルトの設定では、コメントの削除はできますが、追加後に編集をすることはできません。各テーブルで[コメントの編集を許可](../../managers-guide/manage-table/editor/allow-editing-comments/index.md)を有効にすることで、ログインしているユーザ自身が過去に追加したコメントを修正することができるようになります。

## 関連情報

-   [テーブル機能：レコードのエディタ画面](../table/record-authoring/edit-records/table-editor.md)
-   [共通機能：マークダウン](markdown.md)
-   [テーブル機能：レコードの一覧画面](../table/record-authoring/data-analysis/table-grid.md)
-   [サイト機能](../site/index.md)
-   [テーブルの管理：エディタ：コメントの編集を許可](../../managers-guide/manage-table/editor/allow-editing-comments/index.md)
