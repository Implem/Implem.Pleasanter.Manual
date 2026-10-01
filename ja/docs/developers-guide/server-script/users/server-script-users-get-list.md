---
title: users.GetList
icon: material/alpha-m-box
category: サーバスクリプト
order: '25000'
status: ''
parts: ''
urlstring: server-script-users-get-list
shortname: users.GetList
created: 2026-08-25
updated: 2026-09-08
---

## 概要

サーバスクリプトで、絞り込み条件・並び順・ページングを指定して複数のユーザ情報を取得します。

## メソッド

```javascript
users.GetList(view, offset, pageSize);
```

## パラメータ

| パラメータ | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| view       | string | | 絞り込み・並び順条件をJSON形式の文字列で指定します。詳細は「[JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)」を参照してください。省略時は全件が対象になります。 |
| offset     | int | | 取得開始位置（0始まり）。ページングに使用します。詳細は「[JSONデータレイアウト：共通](../../json-data-layout/api-common.md)」の「Offset」を参照してください。 |
| pageSize   | int | | 1回の呼び出しで取得する最大件数。0 または Api.PageSize（既定 200）を超える値を指定した場合は Api.PageSize が適用されます。詳細は「[JSONデータレイアウト：共通](../../json-data-layout/api-common.md)」の「PageSize」を参照してください。 |

## 使用例

### 基本的な使用例（全件・先頭200件）

```javascript
const list = users.GetList();
context.Log(list.Length);
for (const item of list) {
    var user = JSON.parse(item.ToString());
    context.Log(user.UserId + ', ' + user.LoginId + ', ' + user.Name);
}
```

### 絞り込み・並び順・ページングを指定する例

```javascript
const view = {
    ColumnFilterHash: {
        DeptId: '3',
        Disabled: "false"
    },
    ColumnSorterHash: {
        LoginId: 'asc'
    }
};

// 先頭3件のみ取得
const list = users.GetList(JSON.stringify(view), 0, 3);
context.Log('取得件数: ' + list.Length);
```

### キーワード検索（SearchText）の例

```javascript
const view = {
    ColumnFilterHash: {
        SearchText: '山田'
    }
};

const list = users.GetList(JSON.stringify(view));
```

## 戻り値

「userオブジェクト」の配列を返します。オブジェクトのレイアウトは「[開発者ガイド：サーバスクリプト：user](../user/index.md)」を参照してください。該当件数が0件の場合は空配列を返します（null にはなりません）。

```json
[
    {
        "TenantId": 1,
        "UserId": 11,
        "DeptId": 3,
        "LoginId": "yamada",
        "Name": "山田太郎",
        "UserCode": "U0011",
        "TenantManager": false,
        "ServiceManager": false,
        "Disabled": false,
        "ClassHash": {
             "ClassA": "test-class-column"
         },
         "ClassHash": {
            "ClassA": "test-class-column"
        },
        "NumHash": {
            "NumA": 100
        },
        "DateHash": {
            "DateA": "2026-08-19"
        },
        "DescriptionHash": {
            "DescriptionA": "補足説明"
        },
        "CheckHash": {
            "CheckA": true
        }
    }
]
```

## 注意事項
こちらは「[サーバスクリプト](../index.md)」で使用するメソッドです。「[スクリプト](../../script/index.md)」では使用できません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.8.0 以降|機能追加|
