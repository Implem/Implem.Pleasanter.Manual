---
title: $p.apiGet
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-get
translationKey: script-api-get
shortname: $p.apiGet
created: 2019-08-11
updated: 2026-07-15
---

## 概要

指定したサイトのレコード情報を取得します。[サイト統合](../../../users-guide/table/record-authoring/edit-records/table-site-integration.md)を設定しているテーブルの場合は、統合された各レコードの情報もあわせて取得します。

## 制限事項

-   取得できるレコードの件数は[パラメータ設定：Api.json](../../../setup/parameters/api-json.md)の PageSize（デフォルトで200）が最大となります。200件以上のレコードを取得する場合は、「[FAQ：APIで200レコードを超えるデータを取得したい](../../../FAQ/features-for-developers/faq-api-paging.md)」を参照してください。

## 構文

``` js title=JavaScript linenums="1"
$p.apiGet({
    id: <サイトID>,
    data: {
        <取得条件>
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
```

## 各パラメータの説明

| パラメータ名 | 説明                                                                                                                                                                                                                        | 必須 |
| :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--: |
| id           | 操作対象のサイトID、またはレコードIDを指定。                                                                                                                                                                                |  ○   |
| data         | POSTするJSONデータを指定。[JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)、テーブル種類(TableType)を指定することが可能。指定可能なテーブル種類については下記の "テーブル種類について" を確認してください。 |  -   |
| done         | API通信成功時の処理を記述。                                                                                                                                                                                                 |  -   |
| fail         | API通信失敗時の処理を記述。                                                                                                                                                                                                 |  -   |
| always       | API通信の最後に行う処理を記述。                                                                                                                                                                                             |  -   |

### テーブル種類について

テーブル種類（TableType）に指定可能な値は以下の通りです。

| 値               | 説明                                                                                                                                                                                                                     |
| :--------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Normal           | 指定したサイトのレコード情報を取得する場合に指定します。取得するレコード情報は履歴が最新バージョンです。また、こちらの値はTableTypeの既定値で、TableTypeを指定しない場合は、内部ではこの値が設定されて処理が行われます。 |
| History          | 指定したサイトのレコードの履歴情報を取得する場合に指定します。取得するレコード情報は履歴が過去バージョン(最新バージョンは含まない)です。                                                                                 |
| NormalAndHistory | 指定したサイトのレコード情報と履歴情報を合わせて取得する場合に指定します。取得するレコード情報は履歴が全てのバージョンです。                                                                                             |

## 使用例①

POSTするデータに"View"のJSONデータレイアウトを指定する場合は以下のように記述します。

``` js title=JavaScript linenums="1"
$p.apiGet({
    id: 123,
    data: {
        View: {
            ApiDataType: "KeyValues",
            GridColumns: ["Title", "ClassA"]
        }
    },
    done: function (data) {
        alert('通信が成功しました。');
    }
});
```

!!! tip
    "View"のレイアウトについては[JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)を確認してください。

## 使用例②

POSTするデータにテーブル種類"TableType"を指定する場合は以下のように記述します。

``` js title=JavaScript linenums="1"
$p.apiGet({
    id: 123,
    data: {
        TableType: 'History'
    },
    done: function (data) {
        alert('通信が成功しました。');
    }
});
```

## 使用例③

POSTするデータに"View"のJSONデータレイアウト、テーブル種類"TableType"を指定する場合は以下のように記述します。

``` js title=JavaScript linenums="1"
$p.apiGet({
    id: 123,
    data: {
        View: {
            ColumnFilterHash:{
                ClassA: '中野区'
            }
        },
        TableType: 'History'
    },
    done: function (data) {
        console.log(data);
    }
});
```
