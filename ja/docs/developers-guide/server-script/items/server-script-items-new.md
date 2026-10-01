---
title: items.New（非推奨）
icon: material/alpha-m-box
category: サーバスクリプト
order: '0'
status: deprecated
parts: ''
urlstring: server-script-items-new
translationKey: server-script-items-new
shortname: items.New
created: 2021-01-27
updated: 2025-03-04
---

!!! warning "非推奨"
    このメソッドは非推奨となります。[items.NewSite](server-script-items-new-site.md)、[items.NewIssue](server-script-items-new-issue.md)、[items.NewResult](server-script-items-new-result.md)をご利用ください。

## 概要

[サーバスクリプト](../index.md)で「期限付きテーブル」に対する「apiModelオブジェクト」の新規インスタンスを作成します。

## 構文

```
items.New()
```

## 戻り値

「apiModelオブジェクト」を返却します。

## 使用例

下記の例では、サイトID 2 の「期限付きテーブル」にタイトルが "プリザンターのバージョンアップについて" のレコードを作成します。

##### JavaScript

```
let siteId = 2;
let item = items.New();
item.Title = 'プリザンターのバージョンアップについて';
items.Create(siteId, item);
```

## 関連情報

-   [開発者ガイド：サーバスクリプト：items.NewSite](server-script-items-new-site.md)
-   [開発者ガイド：サーバスクリプト：items.NewIssue](server-script-items-new-issue.md)
-   [開発者ガイド：サーバスクリプト：items.NewResult](server-script-items-new-result.md)
-   [開発者ガイド：サーバスクリプト](../index.md)