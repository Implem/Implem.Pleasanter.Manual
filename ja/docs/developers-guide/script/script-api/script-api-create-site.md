---
title: $p.apiCreateSite
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-create-site
translationKey: script-api-create-site
shortname: $p.apiCreateSite
created: 2022-07-05
updated: 2025-10-06
---

## 概要

AjaxのPOSTリクエストにより、サイトを作成します。

## 構文

##### JavaScript

```
$p.apiCreateSite({
    id: (親サイトID),
    data: {
        (作成するサイト情報)
    },
    done: (任意の処理),
    fail: (任意の処理),
    always: (任意の処理)
});
``` 

## 各パラメータの説明

|パラメータ名|説明|必須|
|:--|:--|:--:|
|id|作成するサイトの親サイトIDを指定します。"0"を指定した場合はサイトトップに作成されます。|○|
|data|作成するサイト情報データを指定します。　※欄外補足参照|-|
|done|API通信成功時の処理を記述します。|○|
|fail|API通信失敗時の処理を記述します。|-|
|always|完了時の処理を記述します。|-|

※サイト情報データは、サイトパッケージをエクスポートした際の"Site”パラメータと同等の値を設定する必要があります。[$p.apiGetSite](script-api-get-site.md)でサイト情報を取得したのち、任意の項目を変更してリクエストデータを作成するような処理を想定します。

## 使用例

### 通常の作成

実行ユーザを作成者としてアクセス権を付与します。

```  JavaScript
$p.apiCreateSite({
    id: 123,
    data: {
        ApiVersion: 1.1,
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
});
``` 

### アクセス権の設定を操作したい場合

サイト作成APIでは実行ユーザを作成者としてアクセス権が付与されますが、パラメータ "DisableSiteCreatorPermission" を true に指定することで作成者のアクセス権を無効化することが可能です。
また、パラメータ "Permissions" を指定することで任意のユーザに対してアクセス権を付与することが可能です。

下記の例では、分類A（ユーザの選択肢を設定）が有効化された編集画面で実行されることを前提として、作成者のアクセス権を無効化し、対象ユーザIDに管理者権限（511）を付与しています。
指定可能なアクセス権の数値は、下記ソースコードの「enum Types」に記載されている数値の論理和となります。  
https://github.com/Implem/Implem.Pleasanter/blob/master/Implem.Pleasanter/Libraries/Security/Permissions.cs

##### JavaScript

```
// アクセス権の設定対象ユーザIDを取得する
var targetUserId = $p.getControl('ClassA').attr("data-value");
$p.apiCreateSite({
    id: 123,
    data: {
        ApiVersion: 1.1,
        TenantId: 1,
        Title: 'サイト名',
        ReferenceType: 'Issues',
        ParentId: 99999,
        InheritPermission: 99999,
        DisableSiteCreatorPermission: true,
        Permissions: [
            'User,' + targetUserId + ',511'
        ],
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
});
``` 

### Wikiを作成する場合

##### JavaScript

```
$p.apiCreateSite({
    id: 123,
    data: {
        ApiVersion: 1.1,
        Title: "Wiki名",
        ReferenceType: "Wikis",
        ParentId: 1,
        InheritPermission: 1,
        SiteSettings: {
            Version: 1.017,
            ReferenceType: "Wikis",
            NoDisplayIfReadOnly: false
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
});
```

## 関連情報

-   [$p.apiGetSite](script-api-get-site.md)
