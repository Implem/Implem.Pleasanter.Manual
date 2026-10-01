---
title: 全容量制限(MB)
category: エディタ
order: '6940'
status: ''
parts: ''
urlstring: table-management-limit-total-size
translationKey: table-management-limit-total-size
shortname: 全容量制限
created: 2021-05-23
updated: 2024-06-13
---

## 概要

[添付ファイル項目](../../columns/table-management-attachments.md)の[格納先](table-management-binary-storage-provider.md)が「データベース」または「自動 (データベースまたはローカルフォルダ)」の際に、登録可能なファイルの容量合計の上限値をメガバイト単位で指定します。

## 制限事項

1.  [添付ファイル項目](../../columns/table-management-attachments.md)でのみ設定できます。
1.  [添付ファイル項目](../../columns/table-management-attachments.md)の[格納先](table-management-binary-storage-provider.md)が「データベース」または「自動 (データベースまたはローカルフォルダ)」の場合に設定できます。
1.  本設定は指定した[項目](../../columns/index.md)を対象としたファイル容量制限です。「レコード」単位や[テーブル](../../../../../../users-guide/table/index.md)単位での制限は行えません。
1.  設定可能な範囲は1～1024の間です。設定可能な範囲を変更するには[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「TotalMinSize」および「TotalMaxSize」を変更する必要があります。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 既定値

既定値は1024です。[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「LimitTotalSize」で変更可能です。

## 関連情報

-   [テーブルの管理：項目：添付ファイル](../../columns/table-management-attachments.md)
-   [テーブルの管理：エディタ：項目の詳細設定：格納先](table-management-binary-storage-provider.md)
-   [テーブルの管理：項目](../../columns/index.md)
-   [テーブル機能](../../../../../../users-guide/table/index.md)
-   [パラメータ設定：BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)
