---
title: items.GetSiteByGroupName
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-get-site-by-group-name
translationKey: server-script-items-get-site-by-group-name
shortname: items.GetSiteByGroupName
created: 2023-04-03
updated: 2026-08-05
---

## 概要

[itemsオブジェクト](index.md)の「GetSiteByGroupNameメソッド」です。指定したサイトグループ名をもとにサイト情報を取得します。

## 構文

```
items.GetSiteByGroupName(groupName)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|groupName|object|○|サイトグループ名を指定|

## 戻り値

該当するサイトの[apiModel](../apiModel/server-script-api-model-create.md)の配列を返却します。

## 使用例

以下の例では、サイト名が "SiteAdministrationGroup" のサイト情報を取得します。
```
const sites = Array.from(items.GetSiteByGroupName('SiteAdministrationGroup'));
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