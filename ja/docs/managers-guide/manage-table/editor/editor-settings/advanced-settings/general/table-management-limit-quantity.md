---
title: ファイル数制限
category: エディタ
order: '6920'
status: ''
parts: ''
urlstring: table-management-limit-quantity
translationKey: table-management-limit-quantity
shortname: ファイル数制限
created: 2021-05-23
updated: 2023-04-25
---

## 概要

[添付ファイル項目](../../columns/table-management-attachments.md)に登録可能なファイル数を指定します。

## 制限事項

1.  [添付ファイル項目](../../columns/table-management-attachments.md)でのみ設定できます。
1.  本設定は指定した[項目](../../columns/index.md)単位のファイル数制限のため「レコード」単位や[テーブル](../../../../../../users-guide/table/index.md)単位での制限は行えません。
1.  設定可能な範囲は1～100の間です。設定可能な範囲を変更するには[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「MinQuantity」および「MaxQuantity」を変更する必要があります。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 既定値

既定値は30です。[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「LimitQuantity」で変更可能です。

## 関連情報

-   [テーブルの管理：項目：添付ファイル](../../columns/table-management-attachments.md)
-   [テーブルの管理：項目](../../columns/index.md)
-   [テーブル機能](../../../../../../users-guide/table/index.md)
-   [パラメータ設定：BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)
