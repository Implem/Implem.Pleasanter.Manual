---
title: depts.Update
icon: material/alpha-m-box
category: サーバスクリプト
order: '26020'
status: ''
parts: ''
urlstring: server-script-depts-update
translationKey: server-script-depts-update
shortname: depts.Update
created: 2026-07-22
updated: 2026-09-08
---

## 概要

「[サーバスクリプト](../index.md)」から指定した組織を更新します。[depts](index.md)オブジェクトのメソッドです。

## メソッド

```javascript
depts.Update(deptId, dept);
```

## パラメータ

| パラメータ | 説明                                             | 必須 |
| :--------- | :----------------------------------------------- | :--: |
| deptId     | 更新対象の組織IDを指定します。                   |  ○   |
| dept       | 更新する組織情報をJSON形式の文字列で指定します。 |  ○   |

## 使用例

下記の例では組織ID 2の拡張項目を更新します。

##### JavaScript

```javascript
const deptId = 2;

const payload = {
    ClassHash: {
        ClassA: "test-class-column"
    }
};

depts.Update(deptId, JSON.stringify(payload));
```

## 戻り値

| 型      | 説明                                                               |
| ------- | ------------------------------------------------------------------ |
| boolean | 組織の更新に成功した場合は true、失敗した場合は false を返します。 |

## 拡張項目に値を設定する

「[拡張項目](../../extended-features/extended-column.md)」に値を設定する場合は、ClassHashにカラム名と値を指定します。

##### JavaScript

```javascript
ClassHash: {
    ClassA: "test-class-column"
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.8.0 以降|機能追加|
