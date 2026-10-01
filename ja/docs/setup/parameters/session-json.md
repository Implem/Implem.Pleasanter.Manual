---
title: Session.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: session-json
translationKey: session-json
shortname: Session.json
created: 2019-04-30
updated: 2024-12-10
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|RetentionPeriod|1440|セッションデータの保持期間を分単位で指定。|
|UseKeyValueStore|false|セッションデータの保持に[KVS](../installation/install-database/kvs-install.md)を利用する設定の有効化/無効化をtrue/falseで指定します。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.10.0 以降|UseKeyValueStoreを追加|
