---
title: BackgroundTask.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: background-task-json
translationKey: background-task-json
shortname: BackgroundTask.json
created: 2019-04-30
updated: 2024-09-13
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Enabled|true|バックグラウンドタスクの有効化/無効化を指定。|
|Interval|500|バックグラウンドタスクをサーバサイドで継続的に再実行するまでのインターバルをミリ秒単位で指定。|
|BackgroundTaskSpan|30|バックグラウンドタスクをサーバサイドで継続的に再実行するか判断するための経過時間を秒単位で指定。|
|CreateSearchIndexLot|100|検索インデックスの再作成処理で1度にインデックスを作成するレコードの件数を指定。|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
