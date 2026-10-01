---
title: 容量制限(MB)
category: エディタ
order: '6930'
status: ''
parts: ''
urlstring: table-management-limit-size
translationKey: table-management-limit-size
shortname: 容量制限
created: 2021-05-23
updated: 2024-06-13
---

## 概要

[添付ファイル項目](../../columns/table-management-attachments.md)が「データベース」の際に登録可能な1ファイル当たりの容量の上限値をメガバイト単位で指定します。また、[格納先](table-management-binary-storage-provider.md)が「自動 (データベースまたはローカルフォルダ)」の場合、ファイル単位に保存先の分岐が自動で行われ、システムが保存先を分岐する際に該当ファイルの容量と「容量制限」が比較されます。「容量制限」の指定以下のファイルはデータベース内のBLOBデータとして保存されます。それより大きなファイルはローカルフォルダに保存されます。

## 制限事項

1.  [添付ファイル項目](../../columns/table-management-attachments.md)でのみ設定できます。
1.  [添付ファイル項目](../../columns/table-management-attachments.md)の[格納先](table-management-binary-storage-provider.md)が「データベース」または「自動 (データベースまたはローカルフォルダ)」の場合に設定できます。
1.  設定可能な範囲は1～50の間です。設定可能な範囲を変更するには[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「MinSize」および「MaxSize」を変更する必要があります。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 既定値

既定値は50です。[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「LimitSize」で変更可能です。

## 関連情報

-   [テーブルの管理：項目：添付ファイル](../../columns/table-management-attachments.md)
-   [テーブルの管理：エディタ：項目の詳細設定：格納先](table-management-binary-storage-provider.md)
-   [パラメータ設定：BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)
