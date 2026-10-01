---
title: $p.apiUpdateSite
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-update-site
translationKey: script-api-update-site
shortname: $p.apiUpdateSite
created: 2022-07-05
updated: 2025-10-06
---

## 概要

AjaxのPOSTリクエストにより、サイト情報を更新します。

## 構文

##### JavaScript

```
$p.apiUpdateSite({
    id: (更新対象サイトID),
    data: {
        (更新するサイト情報)
    },
    done: (任意の処理),
    fail: (任意の処理),
    always: (任意の処理)
});
``` 

## 各パラメータの説明

|パラメータ名|説明|必須|
|:--|:--|:--:|
|id|更新対象のサイトID|○|
|data|POSTするJSONデータ　※欄外補足参照|-|
|done|API通信成功|○|
|fail|API通信失敗|-|
|always|完了時|-|

※POSTするJSONデータは、サイトパッケージをエクスポートした際の"Site”パラメータと同等の値を設定する必要があります。[$p.apiGetSite](script-api-get-site.md)でサイト情報を取得したのち、更新したい項目を変更してリクエストデータを作成するような処理を想定します。

## 使用例

##### JavaScript

```
$p.apiUpdateSite({
  id: 123,
  data: {
    TenantId: 1,
    Title: 'サイト名',
    ReferenceType: 'Issues',
    ParentId: 99999,
    InheritPermission: 99999,
    SiteSettings: {
      Version: 1.017,
      ReferenceType: 'Issues',
      GridColumns: [
        'IssueId',
        'TitleBody',
        'Comments',
        'StartTime',
        'CompletionTime',
        'WorkValue',
        'ProgressRate',
        'RemainingWorkValue',
        'Status',
        'Manager',
        'Owner',
        'Updator',
        'UpdatedTime'
      ],
      EditorColumnHash: {
        General: [
          'IssueId',
          'Ver',
          'Title',
          'Body',
          'StartTime',
          'CompletionTime',
          'WorkValue',
          'ProgressRate',
          'RemainingWorkValue',
          'Status',
          'Manager',
          'Owner',
          'Comments'
        ]
      }
    },
    done: function (data) {
      //任意の処理
    },
    fail: function (data) {
      //任意の処理
    },
    always: function (data) {
      //任意の処理
    }
  }
});
``` 

## 関連情報

-   [$p.apiGetSite](script-api-get-site.md)
