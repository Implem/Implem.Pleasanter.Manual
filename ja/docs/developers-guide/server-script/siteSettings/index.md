---
title: siteSettings
icon: material/alpha-o-box
category: サーバスクリプト
order: '3000'
status: ''
parts: ''
urlstring: server-script-site-settings
translationKey: server-script-site-settings
shortname: siteSettings
created: 2021-01-28
updated: 2024-04-19
---

## 概要  

[サーバスクリプト](../index.md)で「サイト設定」の読み取り、変更を行うためのオブジェクトです。

## 制限事項  

1. 「サイト設定の読み取り時」の条件のみ使用できます。

## プロパティ

|No|プロパティ名|変更|説明|
|:--|:----------|:-------:|:---------------------------|
|1|DefaultViewId |○|[既定のビュー](../../../managers-guide/manage-table/grid/table-management-default-view.md)のID|
|2|[Sections](server-script-site-settings-sections.md)|○|Sectionオブジェクトの配列|

## メソッド

|No|Name|Description|
|:----|:----|:----|
|1|[SiteId](server-script-site-settings-site-id.md)|[サイト](../../../users-guide/site/index.md)の[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)をキーに「サイトID」を取得|

## 使用例①

以下の例では、ビューのIDが1のものを既定のビューとして設定します。

##### JavaScript

``` javascript
siteSettings.DefaultViewId = 1;
```

## 使用例②

以下の例では、セクションの情報を取得してセクションのIDとラベルテキストをログに出力します。

##### JavaScript

``` javascript
let sections = siteSettings.Sections;
for (let section of sections) {
    context.Log(`${section.Id} ${section.LabelText}`);
}
```

## 使用例③

以下の例では、サイト名が 部署マスタ のサイトIDを取得してログに出力します。

##### JavaScript

``` javascript
let siteId = siteSettings.SiteId('部署マスタ');
context.Log(siteId);
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：一覧画面：既定のビュー](../../../managers-guide/manage-table/grid/table-management-default-view.md)
-   [開発者ガイド：サーバスクリプト：siteSettings.Sections](server-script-site-settings-sections.md)
-   [開発者ガイド：サーバスクリプト：siteSettings.SiteId](server-script-site-settings-site-id.md)
-   [サイト機能](../../../users-guide/site/index.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../managers-guide/tenant-administration/tenant-logo.md)
