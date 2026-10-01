---
title: items.GetSiteByTitle
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-get-site-by-title
translationKey: server-script-items-get-site-by-title
shortname: items.GetSiteByTitle
created: 2023-03-31
updated: 2023-06-23
---

## 概要

[itemsオブジェクト](index.md)の「GetSiteByTitleメソッド」です。指定したタイトルをもとにサイトの情報を取得します。

## 構文

```
items.GetSiteByTitle(title)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|title|object|○|サイトのタイトルを指定|

## 戻り値

該当するサイトの「apiModel 」の配列を返却します。

## 使用例

以下の例では、タイトルが "部署マスタ" のサイト情報を取得してログに出力します。
```
const sites = Array.from(items.GetSiteByTitle('部署マスタ'));
if (sites.length) {
    sites.forEach(site => {
        context.Log(site.SiteId);
        context.Log(site.Title);
        context.Log(site.ReferenceType);
    })
}
```

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [itemsオブジェクト](index.md)