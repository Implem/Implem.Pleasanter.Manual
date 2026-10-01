---
title: 特定ユーザにのみサイトトップでの新規サイト作成を許可したい
category: FAQ：トップ・サイトメニュー
order: '0'
status: ''
parts: ''
urlstring: faq-disable-top-site-creation
translationKey: faq-disable-top-site-creation
shortname: ''
created: 2019-01-10
updated: 2024-07-01
---

## 回答

[ユーザの管理](../../managers-guide/user-administration/index.md)で許可したいユーザに対して「サイトトップへの作成を許可」のチェックをオンにしてください。

!!! tip "サイトトップとは"
    プリザンターユーザマニュアルでは、サイトトップを「トップ画面」と表記しています。

---

## 概要

特定のユーザにのみサイトトップ（トップ画面）での新規サイト作成を許可します。「サイトトップへの作成を許可」のチェックが入っているユーザのみ、サイトトップにサイトを新規作成できます。

## 制限事項

-   「Pleasanter.net」では設定できません。

## 前提条件

-   [User.json](../../setup/parameters/user-json.md)の「DisableTopSiteCreation」の値がtrueになっていることが必要です。

## 操作方法

1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  [ユーザの管理](../../managers-guide/user-administration/index.md)をクリックしてください。
1.  「サイトトップへの作成を許可」のチェックをオンにしてください。

    ![ユーザの管理の「サイトトップへの作成を許可」のチェックボックス](https://pleasanter.org/files/images/ja/FAQ/top-screen-site-menu/assets/0a28ff6be281416693020a068758cb71.png)

1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。

## 関連情報

-   [ユーザ管理機能](../../managers-guide/user-administration/index.md)
-   [パラメータ設定：User.json](../../setup/parameters/user-json.md)
