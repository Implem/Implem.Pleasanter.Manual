---
title: Slackに通知できるように設定する
category: 追加設定：通知
order: '300'
status: ''
parts: ''
urlstring: slack
translationKey: slack
shortname: ''
created: 2019-04-30
updated: 2024-06-07
---

## 前提条件

slackのユーザ登録およびチームの作成を行ってください。  
https://slack.com/

## Webhook URLの取得

1.以下のURLを開いてください。  
https://slack.com/services/new/incoming-webhook

2.通知先として設定するチャネルを選択し、「Add Incoming WebHooks integration」ボタンをクリックしてください。
![SlackのIncoming WebHooks追加画面。通知先チャネルを選ぶ](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/ebf41a4b1527497a9dd8e019713f6bf5.png)

3.Webhook URLに表示されたURLをコピーしてください。このWebhook URLをプリザンターに設定します。
![SlackのWebhook URLが表示された画面](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/71f488089b074c97ba504a89b24d0bd1.png)

## プリザンターの設定

1.通知を設定するテーブルを選択し、[テーブルの管理](../../../managers-guide/manage-table/index.md)-[通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブを開いてください。「新規作成」ボタンをクリックしてください。
![テーブルの管理の「通知」タブ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/610da5565edd4ff0aacbd22690416a75.png)

2.通知種別を「slack」、アドレスに「Webhook URL」を入力してください。その後、「追加」ボタンをクリックしてください。
![通知の設定画面。通知種別「slack」でアドレスにWebhook URLを入力する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/528cc35d938c419da9e870dc3ea7d874.png)

3.「更新」ボタンをクリックしてください。以上で本手順は完了です。
![テーブルの管理画面。「更新」ボタンで設定を保存する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/0cfe03b7dacd429fb2073a380e24d510.png)