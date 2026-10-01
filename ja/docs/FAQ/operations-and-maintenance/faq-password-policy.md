---
title: アカウントのパスワードポリシーを変更したい
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-password-policy
translationKey: faq-password-policy
shortname: ''
created: 2019-01-22
updated: 2024-04-29
---

## 回答

パラメータファイル[Security.json](../../setup/parameters/security-json.md)の「PasswordPolicies」を変更してください。

---

## 制限事項

パラメータファイル変更後にパスワードを設定・変更した場合に新しいポリシーが適用されます。登録済みのパスワードはそのまま使用できます。

## 概要

パラメータファイル[Security.json](../../setup/parameters/security-json.md)を変更することで、ログインを複数回失敗した場合のアカウントロック設定やパスワード有効期限の設定、パスワードの最低文字数等のパスワードポリシーを変更することができます。パラメータファイルの変更後はIISの再起動を行ってください。

## 関連情報

-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)