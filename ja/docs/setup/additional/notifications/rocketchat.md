---
title: Rocket.Chatに通知できるように設定する
category: 追加設定：通知
order: '700'
status: ''
parts: ''
urlstring: rocketchat
translationKey: rocketchat
shortname: ''
created: 2021-06-17
updated: 2025-01-30
---

## 概要

PleasanterからRocket.Chatに通知するための設定手順です。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。
1. Rocket.Chatの設定、ユーザ登録を行ってください。  
https://rocket.chat/  
1. [Notification.json](../../parameters/notification-json.md)の「Rocket.Chat」をtrueに設定してください。

## Webhook URLの取得

1. Rocket.Chatへログインし、管理（下記画像の赤枠）をクリックしてください。  
![Rocket.Chatの画面。赤枠で示された「管理」のアイコン](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/7adf539910bf4197b3cb648d31b26381.png)

1. 画面左側にある「サービス連携」クリックし、画面右上の「New」をクリックしてください。
![Rocket.Chatの「サービス連携」画面。右上に「New」がある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/c8680c030f9f47cc8e4de7b10a1b31a3.png)

1. 画面右上のボタンでサービス連携を有効にしてください。
![サービス連携の設定画面。右上のボタンで有効にする](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/3a139b2de48648feb4ca9d27d6ebadb4.png)

1. 投稿先チャンネル、投稿ユーザ、その他必要な項目に値を設定し、画面下部にある「保存」をクリックしてください。
![サービス連携の設定画面。投稿先チャンネルや投稿ユーザを設定する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/aa0ad8fc0b1b41b39acd291b39e75686.png)

1. プリザンターに登録するWebhook URLをコピーする。
![発行されたWebhook URLが表示されたRocket.Chatの画面](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/bcbb6f39121141ecb1ca5ed9a6e9ff57.png)

## プリザンターの設定

1.通知を設定するテーブルを選択し、[テーブルの管理](../../../managers-guide/manage-table/index.md)-[通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブを開いてください。「新規作成」ボタンをクリックしてください。
![テーブルの管理の「通知」タブ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/b27648a1885148ba8df02183512da4af.png)

2.通知種別を「Rocket.Chat」、アドレスに「Webhook URL」を入力してください。その後、「追加」ボタンをクリックしてください。
![通知の設定画面。通知種別「Rocket.Chat」でアドレスにWebhook URLを入力する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/285d6e7b5ba4419f8ab9fb0518752b49.png)

3.「更新」ボタンをクリックしてください。以上で本手順は完了です。
![テーブルの管理画面。「更新」ボタンで設定を保存する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/82155cf36f784e90adcda4efe5aecf4a.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.20.0 以降|機能追加|

## 関連情報

-   [パラメータ設定：Notification.json](../../parameters/notification-json.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [応用編：通知、リマインダー](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)