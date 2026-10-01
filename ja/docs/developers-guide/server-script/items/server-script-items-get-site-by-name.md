---
title: items.GetSiteByName
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-get-site-by-name
translationKey: server-script-items-get-site-by-name
shortname: items.GetSiteByName
created: 2023-04-03
updated: 2023-06-23
---

## 概要

[itemsオブジェクト](index.md)の「GetSiteByNameメソッド」です。指定したサイト名をもとにサイトの情報を取得します。

## 前提条件

1. 本機能はサイトの「サイト名」を検索します。あらかじめサイト名を設定してください。サイトの[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)ではありませんので注意ください。
![サイトの「サイト名」を設定する箇所](https://pleasanter.org/files/images/ja/developers-guide/server-script/items/assets/be2492d00d0c4ee0b48cd62f3356ac73.png)

## 構文

```
items.GetSiteByName(name)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|name|object|○|サイト名を指定|

## 戻り値

該当するサイトの「apiModel 」の配列を返却します。

## 使用例

以下の例では、サイト名が "DepartmentMaster" のサイト情報を取得します。
```
const sites = Array.from(items.GetSiteByName('DepartmentMaster'));
if (sites.length) {
    sites.forEach(site => {
        context.Log(site.SiteId);
        context.Log(site.Title);
        context.Log(site.ReferenceType);
    });
}
```

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [itemsオブジェクト](index.md)