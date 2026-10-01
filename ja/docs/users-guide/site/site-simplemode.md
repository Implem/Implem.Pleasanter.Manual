---
title: シンプルモード
category: サイト機能
order: '9'
status: ''
parts: ''
urlstring: site-simplemode
shortname: シンプルモード
created: 2025-03-28
updated: 2025-04-08
---

## 概要
シンプルモードは、サイト（「[フォルダ](../folder/index.md)」、「[テーブル](../table/index.md)」、「[Wiki](../wiki/index.md)」、「[ダッシュボード](../dashboard/index.md)」）の管理画面で利用頻度の高いタブのみを表示する機能です。

## 前提条件
1. この機能を利用するには「パラメータ設定：Site.json」でSimpleModeを有効にする必要があります。

## 操作手順  
1. 対象のサイトを開いてください。  
1. ナビゲーションメニューの「管理」メニューより「フォルダの管理」、「[テーブルの管理](../../managers-guide/manage-table/index.md)」、「Wikiの管理」または「ダッシュボードの管理」をクリックしてください。  
1. シンプルモードが有効の場合、「パラメータ設定：Site.json」の"Tabs"に指定したタブのみが表示されます。

### シンプルモード時
末尾タブの右側の切り替えボタンをクリックすると通常のタブ表示に切り替わります。切り替えボタンは「パラメータ設定：Site.json」の"DisplaySwitch"がtrueの場合のみ表示されます。

![シンプルモードでタブが絞り込まれたサイトの管理画面](https://pleasanter.org/files/images/ja/users-guide/site/assets/5f72866b6d5c41c8afd43710e834c39f.png)

### 通常のタブ表示時
末尾タブの右側の切り替えボタンをクリックするとシンプルモードに切り替わります。切り替えボタンは「パラメータ設定：Site.json」の"DisplaySwitch"がtrueの場合のみ表示されます。

![通常のタブ表示のサイトの管理画面](https://pleasanter.org/files/images/ja/users-guide/site/assets/207eb494566340648068eec36ca154e6.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.15.0以降|機能追加|
