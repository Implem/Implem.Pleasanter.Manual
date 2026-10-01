---
title: LINE WORKSに通知できるように設定する
category: 追加設定：通知
order: '0'
status: ''
parts: ''
urlstring: lineworks
translationKey: lineworks
shortname: ''
created: 2026-01-19
updated: 2026-02-10
---

## 制限事項

1. LINE WORKS側の制約により、追加可能なWebhook URLは5つまでとなっています。

## LINE WORKS側の設定

LINE WORKSの管理者画面より、以下の操作を実施してください。

1. LINE WORKSの「アプリディレクトリ」から[Incoming Webhookアプリ](https://line-works.com/appdirectory/incoming-webhook/)を追加してください。
1. 通知の送信先トークルームへ「Incoming Webhook Bot」を招待してください。
1. 通知の送信先トークルームの「チャンネルID」を取得します。トークルームのメニューから「チャンネルID」を選択してください。  
   ![LINE WORKSのトークルームのメニュー。「チャンネルID」を選ぶ](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/9dedd8090eb54e199fafb6d2194a9e89.png)
1. 「チャンネルIDをコピー」ボタンをクリックしてください。  
   ![「チャンネルIDをコピー」ボタンが表示された画面](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/922d5eba5da8450093d8ecf38f380a50.png)
1. トークルームの下部に表示されるメニューから「Webhook リスト」を選択してください。  
   ![トークルーム下部のメニュー。「Webhook リスト」を選ぶ](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/c859c288d4924e9090c5d6dd68dfdc6c.png)
1. Webhookリスト画面の「追加」でWebhook名を入力し、「チャンネルID」に上記4.でコピーしたチャンネルIDを貼り付け、「追加」ボタンをクリックしてください。  
   ![Webhookリストの追加画面。Webhook名とチャンネルIDを入力する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/a17061c77c5b46da90972f05dc46f704.png)
1. Webhook URLが発行されます。__発行されたWebhook URLは、プリザンター側の設定で使うため、コピーして控えてください。__  
   ![発行されたWebhook URLが表示された画面](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/786e143cb2f9487ab252f59379436430.png)

以上で、LINE WORKS側の設定は完了です。

## プリザンター側の設定

### 1. 通知を設定する

あらかじめ、設定ファイル[Notification.json](../../parameters/notification-json.md)のパラメータLineWorksをtrueに設定してください。設定変更後、プリザンターの再起動が必要です。

1. 通知を設定したいテーブルを開いてください。
1. ナビゲーションメニューの「管理」をクリックしてください。
1. [テーブルの管理](../../../managers-guide/manage-table/index.md)をクリックしてください。
1. [通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブをクリックしてください。
1. 「新規作成」ボタンをクリックしてください。
   ![テーブルの管理の「通知」タブ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/72298cb9a36e4bb3a7ff74669b530b40.png)
1. 「通知種別」から「LINE WORKS」を選択してください。
1. 「アドレス」に、上記でコピーした「Webhook URL」を貼り付けてください。
1. その他、必要な項目を確認し、「追加」ボタンをクリックしてください。

### 2. プロセス通知を設定する

あらかじめ、設定ファイル[Notification.json](../../parameters/notification-json.md)のパラメータLineWorksをtrueに設定してください。設定変更後、プリザンターの再起動が必要です。

1. 通知を設定したいテーブルを開いてください。
1. ナビゲーションメニューの「管理」をクリックしてください。
1. [テーブルの管理](../../../managers-guide/manage-table/index.md)をクリックしてください。
1. [プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)タブをクリックしてください。
1. 「新規作成」ボタンをクリックしてください。
1. [通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブをクリックしてください。
1. 「新規作成」ボタンをクリックしてください。
   ![テーブルの管理の「プロセス」内の「通知」タブ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/a9dfe305dc82410bab84829639520567.png)
1. 「通知種別」から「LINE WORKS」を選択してください。
1. 「アドレス」に、上記でコピーした「Webhook URL」を貼り付けてください。
1. その他、必要な項目を確認し、「追加」ボタンをクリックしてください。

### 3. リマインダーを設定する

あらかじめ、以下の設定を実施してください。

1. 設定ファイル[BackgroundService.json](../../parameters/background-service-json.md)のパラメータReminderをtrueに設定してください。
1. 設定ファイル[Service.json](../../parameters/service-json.md)のパラメータAbsoluteUriに通知やリマインダーに記載されるURLの先頭部分を記入してください。
1. 設定ファイル[Reminder.json](../../parameters/reminder-json.md)のパラメータEnabledをtrueに、LineWorksをtrueに設定してください。

プリザンターの再起動後、以下を実施してください。

1. 通知を設定したいテーブルを開いてください。
1. ナビゲーションメニューの「管理」をクリックしてください。
1. [テーブルの管理](../../../managers-guide/manage-table/index.md)をクリックしてください。
1. [リマインダー](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブをクリックしてください。
1. 「新規作成」ボタンをクリックしてください。
![テーブルの管理の「リマインダー」タブ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/b56fe01c0f174f0bb581d32d66ee2ae4.png)
1. 「リマインダー種別」から「LINE WORKS」を選択してください。
1. 「宛先」に、上記でコピーした「Webhook URL」を貼り付けてください。
1. その他、必要な項目を確認し、「追加」ボタンをクリックしてください。

## 対応バージョン

|対応バージョン|内容|
|-|-|
|1.5.1.0|機能追加|

## 関連情報

-   [Incoming Webhookアプリ](https://line-works.com/appdirectory/incoming-webhook/)
-   [パラメータ設定：Notification.json](../../parameters/notification-json.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [応用編：通知、リマインダー](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)
-   [応用編：プロセスと状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [パラメータ設定：BackgroundService.json](../../parameters/background-service-json.md)
-   [パラメータ設定：Service.json](../../parameters/service-json.md)
-   [パラメータ設定：Reminder.json](../../parameters/reminder-json.md)
