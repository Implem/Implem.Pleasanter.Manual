---
title: _Migratedで始まるテーブルは削除しても良いか
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-migrated-table
translationKey: faq-migrated-table
shortname: ''
created: 2021-04-24
updated: 2024-04-29
---

## 回答

バージョンアップが成功した後はこれらを削除してもプリザンターの動作には影響ありません。

---

## 概要

プリザンターは「バージョンアップ」を行う際にテーブル構成のマイグレーションを行うことがあります。テーブル名が_Migratedで始まるテーブルは、マイグレーション前のテーブル構成およびデータのバックアップです。バージョンアップが成功した後はこれらを削除してもプリザンターの動作には影響ありません。本手順では、バージョンアップで発生した_Migratedで始まる名前のテーブルの削除を行います。

## 注意事項

1. 本手順はデータベースを直接操作するため、危険が伴います。事前に[バックアップ](../backup-restore/faq-backup-and-restore.md)を取得することを強くお勧めします。

## 前提条件

1. SQL Server Management Studioをインストールする必要があります。
1. SQL Server Management Studioをインストールした環境とデータベースの環境が接続可能である必要があります。

## 操作手順

**本手順はSQL ServerおよびMicrosoft AzureのSQL Databaseを利用した環境を対象としています。**

1. SQL Server Management Studioを起動してプリザンターのデータベースサーバに接続してください。
1. 「オブジェクト エクスプローラー」のツリーから「データベース」、「Implem.Pleasanter」、[テーブル](../../users-guide/table/index.md)を展開してください。
1. _Migratedで始まるテーブルを右クリックし、「削除(D)」をクリックしてください。
1. _Migratedで始まるテーブルが削除されたことを確認してください。

## 関連情報

-   [FAQ：プリザンターのDBデータをバックアップする方法とリストアする方法を知りたい](../backup-restore/faq-backup-and-restore.md)
-   [テーブル機能](../../users-guide/table/index.md)