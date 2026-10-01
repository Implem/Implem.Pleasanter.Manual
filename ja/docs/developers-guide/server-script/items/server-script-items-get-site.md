---
title: items.GetSite
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-get-site
translationKey: server-script-items-get-site
shortname: items.GetSite
created: 2023-03-31
updated: 2023-06-23
---

## 概要

[itemsオブジェクト](index.md)の「GetSiteメソッド」です。指定したサイトIDをもとにサイトの情報を取得します。

## 構文

```
items.GetSite(id)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|id|object|○|サイトIDを指定|

## 戻り値

該当するサイトの「apiModel 」の配列を返却します。

## 使用例

以下の例では、サイトID 123 のサイト情報を取得します。
```
const sites = Array.from(items.GetSite(123));
if (sites.length) {
    context.Log(sites[0].SiteId);
    context.Log(sites[0].Title);
    context.Log(sites[0].ReferenceType);
}
```

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [itemsオブジェクト](index.md)