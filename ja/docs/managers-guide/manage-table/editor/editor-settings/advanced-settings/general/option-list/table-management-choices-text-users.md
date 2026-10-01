---
title: ユーザ
category: エディタ
order: '9500'
status: ''
parts: ''
urlstring: table-management-choices-text-users
translationKey: table-management-choices-text-users
shortname: ユーザの選択肢一覧,ユーザ,選択肢一覧
created: 2021-05-02
updated: 2023-04-25
---

## 概要

[選択肢一覧](index.md)に「ユーザ」の一覧を設定します。

## 制限事項

-   [担当者項目](../../../columns/table-management-owner.md)、[管理者項目](../../../columns/table-management-manager.md)、[分類項目](../../../columns/table-management-class.md)以外では使用できません。

## 前提条件

-   設定を行うには「サイトの管理権限」が必要です。

## 記述例

### 記述例1

「ユーザ」の一覧を表示するための記述例です。対象のテーブルにアクセス可能な「ユーザ」のみ表示されます。

``` text title="選択肢一覧"
[[Users]]
```

### 記述例2

「ユーザ」の一覧を表示するための記述例です。すべての「ユーザ」が表示されます。

``` text title="選択肢一覧"
[[Users*]]
```

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](table-management-choices-text-depts.md)
-   [テーブルの管理：項目：担当者](../../../columns/table-management-owner.md)
-   [テーブルの管理：項目：管理者](../../../columns/table-management-manager.md)
-   [テーブルの管理：項目：分類](../../../columns/table-management-class.md)
