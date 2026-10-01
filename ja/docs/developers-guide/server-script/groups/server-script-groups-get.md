---
title: groups.Get
icon: material/alpha-m-box
category: サーバスクリプト
order: '30010'
status: ''
parts: ''
urlstring: server-script-groups-get
shortname: groups.Get
created: 2026-08-25
updated: 2026-09-08
---

## 概要

サーバスクリプトで、グループIDを指定して1件のグループ情報を取得します。

## メソッド

```javascript
groups.Get(groupId);
```

## パラメータ

| パラメータ | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| groupId | long | ○ |取得対象のグループIDを指定します。 |

## 使用例

```javascript
const group = groups.Get(5);
if (group) {
    context.Log(group.GroupName + ', ' + group.Body);
} else {
    context.Log('対象のグループが存在しません。');
}
```

## 戻り値

「groupオブジェクト」を返します。オブジェクトのレイアウトは「[開発者ガイド：サーバスクリプト：group](../group/index.md)」を参照してください。指定したIDのグループが存在しない場合は null を返します。

```json
{
    "TenantId": 1,
    "GroupId": 5,
    "GroupName": "新しいグループ",
    "Body": "dddddd",
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
```

## 注意事項
こちらは「[サーバスクリプト](../index.md)」で使用するメソッドです。「[スクリプト](../../script/index.md)」では使用できません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.8.0 以降|拡張項目の値を取得する機能を追加|
