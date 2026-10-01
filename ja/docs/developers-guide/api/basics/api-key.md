---
title: APIキーの作成
category: API
order: '100'
status: ''
parts: ''
urlstring: api-key
translationKey: api-key
shortname: APIキー
created: 2019-04-30
updated: 2026-08-14
---

## 概要

[API](api.md)を使用するための「APIキー」の発行について説明します。外部プログラムから[API](api.md)を使用するにはユーザ毎に「APIキー」を発行する必要があります。ログインしているブラウザのセッションからアクセスする場合には「APIキー」を指定せずに使用可能です。[API](api.md)で取得するPleasanterの時刻は、「APIキー」を作成したユーザが設定しているタイムゾーンに変更されます。

## 注意事項

1.  「APIキー」が漏洩すると外部プログラムからアクセスが可能となります。「APIキー」は他者に知られないよう厳重に管理してください。

## 操作手順

1.  ナビゲーションメニューより[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)－「API設定」をクリックしてください。
![ナビゲーションメニューのユーザのメニューに表示された「API設定」](https://pleasanter.org/files/images/ja/developers-guide/api/basics/assets/b98b652804b244f89871e518ae3b6835.png)
1.  「作成」ボタンをクリックします。
1.  「APIキー」に表示された文字列がAPIキーです。
![API設定画面。作成された「APIキー」の文字列が表示されている](https://pleasanter.org/files/images/ja/developers-guide/api/basics/assets/a3cd3ef56cff43fbb383812c1005b739.png)

## 関連情報

-   [開発者ガイド：API](api.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
