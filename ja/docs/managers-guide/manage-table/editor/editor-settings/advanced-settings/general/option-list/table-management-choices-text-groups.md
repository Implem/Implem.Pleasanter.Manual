---
title: グループ
category: エディタ
order: '9000'
status: ''
parts: ''
urlstring: table-management-choices-text-groups
translationKey: table-management-choices-text-groups
shortname: グループの選択肢一覧,グループ,選択肢一覧
created: 2021-05-02
updated: 2023-04-25
---

## 概要

[選択肢一覧](index.md)に[グループ](../../../../../../group-administration/index.md)の一覧を設定します。

## 制限事項

-   [分類項目](../../../columns/table-management-class.md)以外では使用できません。

## 前提条件

-   設定を行うには「サイトの管理権限」が必要です。

## 記述例

#### 記述例1

[グループ](../../../../../../group-administration/index.md)の一覧を表示するための記述例です。対象のテーブルにアクセス権が付与されている[グループ](../../../../../../group-administration/index.md)がリストされます。

``` text title="選択肢一覧"
[[Groups]]
```

#### 記述例2

[グループ](../../../../../../group-administration/index.md)の一覧を表示するための記述例です。すべての[グループ](../../../../../../group-administration/index.md)がリストされます。

``` text title="選択肢一覧"
[[Groups*]]
```

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](table-management-choices-text-depts.md)
-   [グループ管理機能](../../../../../../group-administration/index.md)
-   [テーブルの管理：項目：分類](../../../columns/table-management-class.md)