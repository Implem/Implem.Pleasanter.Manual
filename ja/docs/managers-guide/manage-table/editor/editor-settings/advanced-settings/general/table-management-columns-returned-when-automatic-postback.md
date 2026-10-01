---
title: 自動ポストバック時に返却する項目
category: エディタ
order: '11600'
status: ''
parts: ''
urlstring: table-management-columns-returned-when-automatic-postback
translationKey: table-management-columns-returned-when-automatic-postback
shortname: 自動ポストバック時に返却する項目
created: 2021-05-23
updated: 2023-04-25
---

## 概要

[自動ポストバック](table-management-auto-postback.md)を設定した[項目](../../columns/index.md)で[自動ポストバック](table-management-auto-postback.md)が発生した際に、全ての[項目](../../columns/index.md)ではなく特定の[項目](../../columns/index.md)のみを再読込する場合に使用します。1画面の項目数が多くパフォーマンスを改善したい場合に使用します。

## 制限事項

1. [コメント項目](../../columns/table-management-comments.md)では使用できません。
1. [自動ポストバック](table-management-auto-postback.md)を有効化した場合にのみ設定できます。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 操作手順

[エディタの項目の詳細設定](../index.md)を参照してください。

## 設定内容

下記のように項目をカンマ区切りで指定します。[表示名](table-management-label-text.md)は使用できません。

##### Text

```
ClassA,DateA,CheckA
```

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック](table-management-auto-postback.md)
-   [テーブルの管理：項目](../../columns/index.md)
-   [テーブルの管理：項目：コメント](../../columns/table-management-comments.md)
-   [テーブルの管理：エディタ：項目の詳細設定](../index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](table-management-label-text.md)