---
title: サイトの移動
category: サイト機能
order: '4'
status: ''
parts: ''
urlstring: site-move
shortname: ''
created: 2021-04-12
updated: 2026-03-10
---

## 概要
対象のサイトを上位のフォルダや下位のフォルダ配下に移動します。

## 制限事項
1. フォルダの移動を行ってもアクセス権の継承関係は変更されません。上位フォルダからアクセス権を継承して作成したフォルダを上位フォルダよりも更に上位に移動しても、アクセス権の継承はそのままとなります。

## 前提条件
1. 移動対象のサイト、移動対象の上位サイトおよび移動先のサイトに「サイトの管理権限」が必要です。

## 操作手順
1. サイトをドラッグ&ドロップにより移動します。フォルダにドロップすることで下位に移動します。「上へ」ドロップすることで上位に移動します。

![サイトをドラッグ＆ドロップで別のフォルダへ移動する操作](https://pleasanter.org/files/images/ja/users-guide/site/assets/1a03f546d3b145fca17e86ca8faef822.png)

## トップ画面におけるサイトの移動
トップ画面からの移動およびトップ画面への移動についてはそれぞれ以下の条件が必要となります。

### トップ画面から下位フォルダ配下へのサイトの移動
- [User.json](../../setup/parameters/user-json.md)のDisableMovingFromTopSiteがfalseであること。または「User.json」のDisableMovingFromTopSiteがtrueでかつ「[ユーザの管理](../../managers-guide/user-administration/index.md)」で「サイトトップからの移動を許可」が有効であること
- 移動するサイトに対して「サイトの管理権限」が付与されていること
- 移動先の下位フォルダに対して「サイトの管理権限」が付与されていること

### 下位フォルダからトップ画面へのサイトの移動
- [User.json](../../setup/parameters/user-json.md)のDisableTopSiteCreationがfalseであること。または「User.json」のDisableTopSiteCreationがtrueでかつ「[ユーザの管理](../../managers-guide/user-administration/index.md)」で「サイトトップへの作成を許可」が有効であること
- 移動するサイトに対して「サイトの管理権限」が付与されていること
