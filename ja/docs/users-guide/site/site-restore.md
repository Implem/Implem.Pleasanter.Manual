---
title: サイトをゴミ箱から復元
category: サイト機能
order: '7'
status: ''
parts: ''
urlstring: site-restore
shortname: ''
created: 2019-06-30
updated: 2024-06-03
---

## 概要
削除した「[サイト](index.md)」をごみ箱から復元します。

## 制限事項
1. ごみ箱から削除したサイトは復元できません。
1. 復元したサイトの配下にある情報（フォルダ、テーブル、レコード）は復元されないため、下図のように「フォルダＡ」を復元する場合には「フォルダＡ」→「テーブルＡ」→「テーブルＡ - レコード」のように上位サイトから順に復元する必要があります。  

![「フォルダＡ」を復元する例を示したサイトの階層図](https://pleasanter.org/files/images/ja/users-guide/site/assets/5f3f4790adc04368b14b4940db9036c7.png)

## 前提条件
1. 「サイトの管理」権限が必要です。
1. トップのサイトを復元する場合には「[特権ユーザ](../../managers-guide/user-administration/user-management-privileged-users.md)」権限が必要です。

## 操作手順
1. 削除されたサイトが格納されていたフォルダに移動してください。
1. 「管理」メニューから「ごみ箱」をクリックしてください。
1. 復元対象のサイトにチェックし「復元」ボタンをクリックしてください。
1. 確認ダイアログが表示されるので「OK」ボタンをクリックしてください。

![ごみ箱でサイトにチェックを付けて復元する画面](https://pleasanter.org/files/images/ja/users-guide/site/assets/e7439eed3df4496190dee0aa3b64754c.png)
