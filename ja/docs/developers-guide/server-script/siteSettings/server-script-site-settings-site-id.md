---
title: siteSettings.SiteId
icon: material/alpha-m-box
category: サーバスクリプト
order: '3010'
status: ''
parts: ''
urlstring: server-script-site-settings-site-id
translationKey: server-script-site-settings-site-id
shortname: siteSettings.SiteId
created: 2021-10-18
updated: 2023-06-21
---

## 概要

[siteSettingsオブジェクト](index.md)のSiteIdメソッドです。[サーバスクリプト](../index.md)で[サイト](../../../users-guide/site/index.md)の[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)をキーに「サイトID」を取得します。

## 構文

``` javascript
siteSettings.SiteId(title);
```

## パラメータ

|No|パラメータ|型|必須|概要|
|:--|:----------|:----------|:---:|:---------------------------|
|1|title|string|○|取得する[サイト](../../../users-guide/site/index.md)の[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)|

## 戻り値

`long`型の「サイトID」を返却します。指定した[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)の[サイト](../../../users-guide/site/index.md)が見つからない場合には 0 を返却します。

## 使用例

下記の例では[サイト](../../../users-guide/site/index.md)の[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)が My site title の[サイト](../../../users-guide/site/index.md)の「サイトID」を取得します。

##### JavaScript

``` javascript
siteSettings.SiteId('My site title');
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [サイト機能](../../../users-guide/site/index.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../managers-guide/tenant-administration/tenant-logo.md)
