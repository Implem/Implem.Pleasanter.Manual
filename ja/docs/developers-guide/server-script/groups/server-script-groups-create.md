---
title: groups.Create
icon: material/alpha-m-box
category: サーバスクリプト
order: '30010'
status: ''
parts: ''
urlstring: server-script-groups-create
translationKey: server-script-groups-create
shortname: groups.Create
created: 2026-07-21
updated: 2026-09-08
---

## 概要

「[サーバスクリプト](../index.md)」から新しいグループを作成します。[groups](index.md)オブジェクトのメソッドです。

## メソッド

```javascript
groups.Create(group);
```

## パラメータ

| パラメータ | 説明                                                 | 必須 |
| :--------- | :--------------------------------------------------- | :--: |
| group      | 作成するグループ情報をJSON形式の文字列で指定します。 |  ○   |

## 使用例

下記の例では新しいグループを作成します。

```javascript
(function () {
    const group = {
        GroupName: "新しいグループ",
        Body: "dddddd",
        Disabled: false,
        Comments: "created-by-server-script",
        ClassHash: {
            ClassA: "test-class-column"
        }
    };

    const ok = groups.Create(JSON.stringify(group));
    context.Log("groups.Create returned:", ok);
})();
```

## 戻り値

| 型      | 説明                                                                |
| ------- | ------------------------------------------------------------------- |
| boolean | グループの作成に成功した場合はtrue、失敗した場合はfalseを返します。 |

## 拡張項目に値を設定する

「[拡張項目](../../extended-features/extended-column.md)」に値を設定する場合は、ClassHashにカラム名と値を指定してください。

```javascript
ClassHash: {
    ClassA: "test-class-column"
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.8.0 以降|機能追加|
