---
title: items.NewSite
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-new-site
translationKey: server-script-items-new-site
shortname: items.NewSite
created: 2023-07-31
updated: 2026-09-02
---

## 概要

[サーバスクリプト](../index.md)で[サイト](../../../users-guide/site/index.md)に対する「apiModelオブジェクト」の新規インスタンスを作成します。

## 構文

```
items.NewSite(referenceType)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|referenceType|string|○|サイト種別を指定。<br>”Sites”：サイト<br>"Issues"：期限付きテーブル<br>"Results"：記録テーブル<br>"Wikis"：Wiki<br>"DashBoard"：ダッシュボード|

## 戻り値

[サイト](../../../users-guide/site/index.md)の「apiModelオブジェクト」を返却します。

## 使用例①

下記の例では、トップページ（サイトID 0）に"プリザンター"という名称の[フォルダ](../../../users-guide/folder/index.md)を作成します。

##### JavaScript

```
let siteId = 0;
let item = items.NewSite("Sites");
item.Title = 'プリザンター';
items.Create(siteId, item);
context.Log(item.SiteId); // 作成したサイトのIDを出力
```

## 使用例②

下記の例では、サイトID 2に"課題管理"という名称の「期限付きテーブル」を作成します。items.Createを利用します。

##### JavaScript

```
let siteId = 2;
let item = items.NewSite("Issues");
item.Title = '課題管理';
let siteSettings = {}
item.SiteSettings = $ps.JSON.stringify(siteSettings);
items.Create(siteId, item);
context.Log(item.SiteId); // 作成したサイトのIDを出力
```

## 使用例③

下記の例では、サイトID 2に"顧客管理"という名称の「記録テーブル」を作成します。apiModel.Createを使用します。

##### JavaScript

```
let siteId = 2;
let apiModel= items.NewSite("Results");
apiModel.Title = '顧客管理';
let siteSettings = {}
apiModel.SiteSettings = $ps.JSON.stringify(siteSettings);
apiModel.Create(siteId);
context.Log(apiModel.SiteId); // 作成したサイトのIDを出力
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [サイト機能](../../../users-guide/site/index.md)
-   [フォルダ機能](../../../users-guide/folder/index.md)