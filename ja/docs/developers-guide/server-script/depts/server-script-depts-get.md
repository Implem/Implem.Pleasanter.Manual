---
title: depts.Get
icon: material/alpha-m-box
category: サーバスクリプト
order: '26020'
status: ''
parts: ''
urlstring: server-script-depts-get
shortname: depts.Get
created: 2026-08-25
updated: 2026-09-08
---

## 概要

サーバスクリプトで、組織IDを指定して1件の組織情報を取得します。

## メソッド

```javascript
depts.Get(deptId);
```

## パラメータ

| パラメータ | 型     | 必須 | 説明 |
| ---------- | ------ | ---- | ------------------------------ |
| deptId     | long | ○ | 取得対象の組織IDを指定します。 |

## 使用例

```javascript
const dept = depts.Get(2);
if (dept) {
    context.Log(dept.DeptCode + ', ' + dept.DeptName);
} else {
    context.Log('対象の組織が存在しません。');
}
```

## 戻り値

「deptオブジェクト」を返します。オブジェクトのレイアウトは「[開発者ガイド：サーバスクリプト：dept](../dept/index.md)」を参照してください。指定したIDの組織が存在しない場合は null を返します。

```json
{
    "TenantId": 1,
    "DeptId": 2,
    "DeptCode": "D001",
    "DeptName": "新しい部署",
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

