---
title: ナビゲーションメニューに「パスワード変更」メニューを表示したい
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-show-change-password-menu
translationKey: faq-show-change-password-menu
shortname: ''
created: 2022-02-16
updated: 2024-07-01
---

## 回答

[Service.json](../../setup/parameters/service-json.md)の「ShowChangePassword」をtrueにしてください。

---

## 概要

ナビゲーションメニューに「パスワード変更」メニューを表示する条件が変更になりました。

## 詳細情報

ナビゲーションメニューに「パスワード変更」メニューを表示する条件が、下記の通り変更になりました。
以前は[Service.json](../../setup/parameters/service-json.md)の「ShowChangePassword」および「ShowProfiles」の両方をtrueにする必要がありましたが、今後は「ShowChangePassword」のみをtrueにすることで「パスワード変更」メニューが表示されます。
![ナビゲーションメニューに「パスワード変更」が表示されている状態](https://pleasanter.org/files/images/ja/FAQ/others/assets/acda2a0de0b7472ba133206e989e243b.png)

## 関連情報

-   [パラメータ設定：Service.json](../../setup/parameters/service-json.md)