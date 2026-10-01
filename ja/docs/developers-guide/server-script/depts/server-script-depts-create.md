---
title: depts.Create
icon: material/alpha-m-box
category: サーバスクリプト
order: '26010'
status: ''
parts: ''
urlstring: server-script-depts-create
translationKey: server-script-depts-create
shortname: depts.Create
created: 2026-07-22
updated: 2026-09-08
---

## 概要

「[サーバスクリプト](../index.md)」から新しい「[組織](../../../managers-guide/department-administration/index.md)」を作成します。[depts](index.md)オブジェクトのメソッドです。

## メソッド

```javascript
depts.Create(dept);
```

## パラメータ

| パラメータ | 説明                                             | 必須 |
| :--------- | :----------------------------------------------- | :--: |
| dept       | 作成する組織情報をJSON形式の文字列で指定します。 |  ○   |

## 使用例

下記の例では新しい組織を作成します。

```javascript
const payload = {
    DeptCode: "D001",
    DeptName: "新しい組織",
    Body: "説明",
    Disabled: false,
    ClassHash: {
        ClassA: "test-class-column"
    }
};

const createok = depts.Create(JSON.stringify(payload));
context.Log(createok);
```

## 戻り値

| 型      | 説明                                                            |
| :------ | :-------------------------------------------------------------- |
| boolean | 組織の作成に成功した場合はtrue、失敗した場合はfalseを返します。 |

## 拡張項目に値を指定する

「[拡張項目](../../extended-features/extended-column.md)」に値を設定する場合は、ClassHashにカラム名と値を指定します。

```javascript
ClassHash: {
    ClassA: "test-class-column"
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.8.0 以降|機能追加|
