---
title: 検索インデックスをバッチ処理で再構築したい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: rebuild-search-indexes
translationKey: rebuild-search-indexes
shortname: バッチから検索インデックスを再構築
created: 2022-04-25
updated: 2024-04-29
---

## 回答

「[検索インデックス再構築](../../developers-guide/api/site-operations/api-rebuild-search-indexes.md)」用のAPIを実行してください。

---

## 概要

バッチ処理などで登録したデータに対しては「検索インデックス」が作成されない場合があります。その場合、画面から「[検索インデックスの再構築](../../managers-guide/manage-table/search/table-management-rebuild-search-indexes.md)」を実行する必要がありますが、バッチ処理内で「[検索インデックス再構築](../../developers-guide/api/site-operations/api-rebuild-search-indexes.md)」APIを実行することで、インデックスの再構築を実行することができます。

## 前提条件

1. パラメータ[BackgroundTask.json](../../setup/parameters/background-task-json.md)の「Enabled」をtrueにする必要があります。

## 操作方法

1. バッチ処理内で「[検索インデックス再構築](../../developers-guide/api/site-operations/api-rebuild-search-indexes.md)」APIを実行してください。

## スクリプト例

PowerShellで検索インデックス再構築APIを実行します。

#### PowerShell

```
$params = @{
    "ApiVersion": 1.1;
    "ApiKey": "xxxxx...";
}
$response = Invoke-RestMethod -Uri http://{サーバー名}/api/BackgroundTasks/{サイトID}/RebuildSearchIndexes -Method POST -Body ($params|ConvertTo-Json) -ContentType "application/json";
```
※{サーバー名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。
