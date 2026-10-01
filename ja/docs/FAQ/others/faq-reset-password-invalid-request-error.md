---
title: パスワード初期化後やユーザの管理を開く際に「不正なリクエストが送信されました」と表示される
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-reset-password-invalid-request-error
translationKey: faq-reset-password-invalid-request-error
shortname: ''
created: 2020-05-27
updated: 2024-04-29
---

## 回答

[Service.json](../../setup/parameters/service-json.md)の「ShowProfiles」がtrueになっているか確認してください。

---

## 概要

Service.jsonのShowProfilesがfalseになっている場合、一旦trueに変更してからパスワードの変更処理などを実行してください。

## 関連情報

-   [パラメータ設定：Service.json](../../setup/parameters/service-json.md)