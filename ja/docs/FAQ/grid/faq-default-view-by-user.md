---
title: ログインユーザごとに既定のビューを変更したい
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-default-view-by-user
translationKey: faq-default-view-by-user
shortname: ''
created: 2021-01-20
updated: 2024-07-08
---

## 回答

[サーバスクリプト](../../developers-guide/server-script/index.md)を使用してください。

---

## 概要

表示される一覧画面のビューをログインユーザごとに変更します。ユーザIDが1の場合はビューIDが1、ユーザIDが2の場合はビューIDが2、それ以外のユーザにはビューIDが3のビューを[既定のビュー](../../managers-guide/manage-table/grid/table-management-default-view.md)に設定します。

## 操作手順

1. 「記録テーブル」を作成します。
1. [テーブルの管理](../../managers-guide/manage-table/index.md)→[ビュー](../../users-guide/hands-on/advanced/advanced-operations-view.md)で新規のビューを作成します。  
1. 対象のユーザIDとビューIDを事前にメモしておいてください。ユーザIDはナビゲーションメニューの「管理」－[ユーザの管理](../../managers-guide/user-administration/index.md)から、ビューIDはナビゲーションメニューの「管理」→[テーブルの管理](../../managers-guide/manage-table/index.md)→[ビュー](../../users-guide/hands-on/advanced/advanced-operations-view.md)→「詳細設定」からそれぞれ確認してください。
    ![ユーザの管理画面でユーザIDを確認するところ](https://pleasanter.org/files/images/ja/FAQ/grid/assets/50c58c8859234d95a6c2393d113db620.png)
    ![ビューの詳細設定でビューIDを確認するところ](https://pleasanter.org/files/images/ja/FAQ/grid/assets/197d65f53b8b4a3e8ecf19186b5b9cd3.png)

1. 以下の[サーバスクリプト](../../developers-guide/server-script/index.md)を「新規作成」します。  [条件](../../developers-guide/server-script/basics/server-script-conditions.md)は「サイト設定の読み込み時」を選択します。

## スクリプト

##### JavaScript

```
if (context.UserId === 1) {   //ユーザIDが1の場合
    siteSettings.DefaultViewId = 1;   //既定のビューをIDが1のビューに設定する
} else if (context.UserId === 2) {   //ユーザIDが2の場合
    siteSettings.DefaultViewId = 2;   //既定のビューをIDが2のビューに設定する
} else {   //ユーザIDが上記以外の場合
    siteSettings.DefaultViewId = 3;   //既定のビューをIDが3のビューに設定する
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
-   [テーブルの管理：一覧画面：既定のビュー](../../managers-guide/manage-table/grid/table-management-default-view.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [応用編：ビュー](../../users-guide/hands-on/advanced/advanced-operations-view.md)
-   [ユーザ管理機能](../../managers-guide/user-administration/index.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../editor/faq-condition-mode-range.md)