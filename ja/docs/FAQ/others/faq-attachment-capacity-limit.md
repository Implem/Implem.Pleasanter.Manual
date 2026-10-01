---
title: 添付ファイルの容量制限をテーブル毎ではなく、すべてのテーブルに対して一括で設定したい
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-attachment-capacity-limit
translationKey: faq-attachment-capacity-limit
shortname: ''
created: 2019-03-27
updated: 2024-04-29
---

## 回答

パラメータ[BinaryStorage.json](../../setup/parameters/binary-storage-json.md)で一括で設定可能です。

---

## 概要

パラメータ[BinaryStorage.json](../../setup/parameters/binary-storage-json.md)の「LimitSize」、「LimitTotalSize」、「LocalFolderLimitSize」、「LocalFolderLimitTotalSize」を変更することですべてのテーブルに対して添付ファイルの容量制限を行うことができます。既にテーブル毎に添付ファイルの容量制限を行っていた場合はそちらの設定が優先されますが、初期値から変更していない場合は[BinaryStorage.json](../../setup/parameters/binary-storage-json.md)の初期値の設定が反映されます。

## 関連情報

-   [パラメータ設定：BinaryStorage.json](../../setup/parameters/binary-storage-json.md)
