---
title: ローカルフォルダ容量制限(MB)
category: エディタ
order: '6950'
status: ''
parts: ''
urlstring: table-management-local-folder-limit-size
translationKey: table-management-local-folder-limit-size
shortname: ローカルフォルダ容量制限
created: 2021-05-24
updated: 2024-06-13
---

## 概要

[添付ファイル項目](../../columns/table-management-attachments.md)の[格納先](table-management-binary-storage-provider.md)が「ローカルフォルダ」の際に登録可能な1ファイル当たりの容量の上限値をメガバイト単位で指定します。また、[格納先](table-management-binary-storage-provider.md)が「自動 (データベースまたはローカルフォルダ)」の場合、ファイルの保存先としてローカルフォルダが自動で選択された際に保存できるファイル単位の容量の上限値を「ローカルフォルダ容量制限」に指定してください。

## 制限事項

1.  [添付ファイル項目](../../columns/table-management-attachments.md)でのみ設定できます。
1.  [添付ファイル項目](../../columns/table-management-attachments.md)の[格納先](table-management-binary-storage-provider.md)が「ローカルフォルダ」または「自動 (データベースまたはローカルフォルダ)」の場合に設定できます。
1.  設定可能な範囲は1～3072の間です。設定可能な範囲を変更するには[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「LocalFolderMinSize」および「LocalFolderMaxSize」を変更する必要があります。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 既定値

既定値は3072です。[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「LocalFolderLimitSize」で変更可能です。

## 関連情報

-   [テーブルの管理：項目：添付ファイル](../../columns/table-management-attachments.md)
-   [テーブルの管理：エディタ：項目の詳細設定：格納先](table-management-binary-storage-provider.md)
-   [パラメータ設定：BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)
