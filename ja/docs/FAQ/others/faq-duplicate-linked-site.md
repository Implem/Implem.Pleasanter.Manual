---
title: リンクされた複数のサイトをリンク関係を保ったまま複製したい
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-duplicate-linked-site
translationKey: faq-duplicate-linked-site
shortname: サイトパッケージの複製
created: 2024-02-09
updated: 2024-12-12
---

## 回答

[サイトパッケージのエクスポート](../../managers-guide/manage-table/site-package/site-package-export.md)と[サイトパッケージのインポート](../../managers-guide/manage-table/site-package/site-package-import.md)を使用してください。

---

## 概要

リンクされた複数のサイトを同じフォルダ内に配置してください。その後、フォルダ階層から[サイトパッケージをエクスポート](../../managers-guide/manage-table/site-package/site-package-export.md)し、そのまま[サイトパッケージをインポート](../../managers-guide/manage-table/site-package/site-package-import.md)することで、リンク関係を保ったまま複製できます。

また、データを含めエクスポート・インポートすれば、データも同様にリンク関係を保ったまま複製されます。

更に、指定書式で記載することで、[スクリプト](../../managers-guide/manage-table/scripts/index.md)と[サーバスクリプト](../../developers-guide/server-script/index.md)もリンク関係を保持したまま複製できます。

### リンクの親子関係の説明

![リンクの親子関係を示した図](https://pleasanter.org/files/images/ja/FAQ/others/assets/d50d7f3b86234d9799718fc3be4e5323.png)

## 制限事項

-   [スクリプト](../../managers-guide/manage-table/scripts/index.md)・[サーバスクリプト](../../developers-guide/server-script/index.md)処理文内のID置換はver.1.4.9.0以降で使用できます。

## スクリプト・サーバスクリプト処理文内のID置換の書式

<!-- meta version="1.4.9.0" -->

[スクリプト](../../managers-guide/manage-table/scripts/index.md)と[サーバスクリプト](../../developers-guide/server-script/index.md)処理内で`// @siteid list start@`と`// @siteid list end@`で囲まれた範囲内の数値型文字列が、インポート後のサイトIDに置換されます。**`// @siteid list start@`は必ず行頭に記載してください。**

``` js hl_lines="1 4"
// @siteid list start@
const siteId = 1000;
const tableIds = [1001,1002,1003,1004];
// @siteid list end@

/* 以下省略 */ 
```

### ID置換の例

サイトパッケージインポート後、サイトIDが2000から採番された例です。

#### 置換前（サイトパッケージ内部の状態）

```js hl_lines="1 4"
// @siteid list start@
const sitePC = 1000;
const masterOS = [1001,1002,1003,1004];
// @siteid list end@
const wiki = 1005;

// 以降でconstの値を使用して処理を行う。
if (sitePc == $p.id())  { /* 何かしらの処理 */ }
```

#### 置換後（インポート後のプリザンター内部の状態）

`// @siteid list start@`と`// @siteid list end@`で囲まれた数値が、インポート後のサイトIDに置換されます。範囲外の数値（`wiki = 1005`）は置換されません。

```js hl_lines="1 4"
// @siteid list start@
const sitePC = 2000;
const masterOS = [2001,2002,2003,2004];
// @siteid list end@
const wiki = 1005;

// 以降でconstの値を使用して処理を行う。
if (sitePc == $p.id())  { /* 何かしらの処理 */ }
```

## 関連情報

-   [テーブルの管理：サイトパッケージ：サイトパッケージのエクスポート](../../managers-guide/manage-table/site-package/site-package-export.md)
-   [テーブルの管理：サイトパッケージ：サイトパッケージのインポート](../../managers-guide/manage-table/site-package/site-package-import.md)
-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
