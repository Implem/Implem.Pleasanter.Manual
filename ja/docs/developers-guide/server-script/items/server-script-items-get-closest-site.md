---
title: items.GetClosestSite
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-get-closest-site
translationKey: server-script-items-get-closest-site
shortname: items.GetClosestSite,GetClosestSite,サイト名検索
created: 2024-06-05
updated: 2026-06-23
---

## 概要

[itemsオブジェクト](index.md)の「GetClosestSiteメソッド」です。[サイト名検索](../../api/site-operations/api-site-get-closest-siteid.md)で該当サイトに最も近いサイト情報を取得します。

## 前提条件

1. 本機能はサイトの「サイト名」を検索します。あらかじめサイト名を設定してください。サイトの[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)ではありませんので注意ください。
![サイトの「サイト名」を設定する箇所](https://pleasanter.org/files/images/ja/developers-guide/server-script/items/assets/be2492d00d0c4ee0b48cd62f3356ac73.png)

## 構文

```
items.GetClosestSite(name,id)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|name|string|○|サイト名を指定|
|id|int||検索開始サイトIDを指定（省略時：サーバスクリプトが格納されたサイトID）|

## 戻り値

該当するサイトの[apiModel](../apiModel/server-script-api-model-create.md)を返却します。
見つからなかった場合またはアクセス権が無い場合はnullを返却します。

## 使用例

以下の例では、サイト名が "WBS" のサイト情報を取得します。
```
const site = items.GetClosestSite('WBS');
if (site) {
	context.Log(site.SiteId);
	context.Log(site.Title);
	context.Log(site.ReferenceType);
}
```

## 使用例①

以下の例では、[サーバスクリプト](../index.md)が格納されたサイトからサイト名”WBS”で検索したサイト情報を取得します。
```
const site = items.GetClosestSite('WBS');
```

## 使用例②

以下の例では、サイトIDが1234のサイトからサイト名”WBS”で検索したサイト情報を取得します。
[バックグラウンドサーバスクリプト](../../../managers-guide/tenant-administration/background-server-script.md)ではこちらを使用します。
```
const site = items.GetClosestSite('WBS',1234);
```

## サンプルコード

<details markdown="1">
<summary>1. サイトIDをキャッシュし処理効率化</summary>

サイトIDをキャッシュ、2回目以降使用する際はキャッシュから取得することで、処理効率化を図ります。

```javascript
// サイトIDキャッシュ
const _siteIdCache = new Map();
// サイト名からSiteIdを取得（キャッシュ）
function getSiteIdOrNull(siteName) {
    if (_siteIdCache.has(siteName)) return _siteIdCache.get(siteName);
    const site = items.GetClosestSite(siteName);
    if (!site || !site.SiteId) {
        logs.LogUserError(
            `${siteName} サイト情報取得失敗`,
            getSiteIdOrNull.name,
        );
        return null;
    }
    _siteIdCache.set(siteName, site.SiteId);
    return site.SiteId;
}
const siteId = getSiteIdOrNull('案件管理');
if (siteId) {
    logs.LogInfo(`案件管理のSiteId: ${siteId}`);
}
```

</details>

## 補足

「[開発者ガイド：サーバスクリプト：items.GetSiteByName](server-script-items-get-site-by-name.md)」との違いは、items.GetSiteByNameメソッドは該当サイト名を持つ全てのサイトを返しますが、item.GetClosestSiteメソッドは検索開始サイトから最近傍の該当サイト名を持つサイトを１つ返します。

## 関連情報

-   [開発者ガイド：サーバスクリプト：items](index.md)
-   [開発者ガイド：API：サイト操作：サイト名検索で該当サイトに最も近いサイトID取得](../../api/site-operations/api-site-get-closest-siteid.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../managers-guide/tenant-administration/tenant-logo.md)
-   [開発者ガイド：サーバスクリプト：apiModel.Create](../apiModel/server-script-api-model-create.md)
-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テナント管理機能：バックグラウンドサーバスクリプト](../../../managers-guide/tenant-administration/background-server-script.md)