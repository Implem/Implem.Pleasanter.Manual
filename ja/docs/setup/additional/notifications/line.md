---
title: LINEに通知できるように設定する
category: 追加設定：通知
order: '500'
status: ''
parts: ''
urlstring: line
translationKey: line
shortname: ''
created: 2019-04-30
updated: 2025-10-29
---

## プリザンターでLINE通知の設定を行う

まず、LINE通知機能の設定前に以下の内容を準備しておきます。

1. 通知送信用のBotアカウントの作成  
　以下のLINE Developersのドキュメントを参照し、通知送信用のBotアカウントを作成してください。  
  [ボットを作成する | LINE Developers](https://developers.line.biz/ja/docs/messaging-api/building-bot/)
1. Botアカウントを友達登録するためのQRコード  
　[LINE Developersコンソール](https://developers.line.me/console/)のMessaging APIチャネルにあるMessaging API設定タブに移動し、表示されているQRコードを使用します。  
　（QRコードの画像をPCに保存（ブラウザでQRコードを右クリック⇒保存）し、メールに添付する等の方法で通知を受け取るユーザに配布しておきます。）
1. Botアカウントのアクセストークン  
 　 [LINE Developersコンソール](https://developers.line.me/console/)のMessaging APIチャネルにあるMessaging API設定タブに移動し、Botアカウントの「チャネルアクセストークン（長期）」を控えておきます。

## サイト設定にLINE通知を設定する

### 個々のユーザに対して通知を行う場合

1. 以下のLINE Developersのドキュメントを参照し、通知先のユーザのユーザIDを取得してください。  
　[ユーザIDを取得する | LINE Developers](https://developers.line.biz/ja/docs/messaging-api/getting-user-ids/)
1. メニュー[管理]-[テーブルの管理]を選択し、[通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブ内の「新規作成」ボタンをクリックします。  
1. 「通知種別」で"LINE"を選択します。
1. 「アドレス」欄に確認したユーザIDを入力します。ユーザIDはカンマ区切りで複数設定可能です。
1. 「トークン」欄に、Botアカウントのアクセストークンを入力します。

![通知の設定画面。通知種別「LINE」でユーザIDとトークンを入力する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/8f9c3467bde140468aee3dd2dd30ae39.png)

### LINEグループに対して通知を行う場合

1. LINEのWebhook機能をご利用いただき、通知先のグループのグループIDを取得してください。  
　[メッセージ（Webhook）を受信する | LINE Developers](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/)
1. メニュー[管理]-[テーブルの管理]を選択し、[通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブ内の「新規作成」ボタンをクリックします。  
1. 「通知種別」で"LINEグループ"を選択します。
1. 「アドレス」欄に確認したグループIDを入力します。グループIDは1つのみ設定可能です。カンマ区切りで複数設定することはできません。
1. 「トークン」欄に、Botアカウントのアクセストークンを入力します。

![通知の設定画面。通知種別「LINEグループ」でグループIDとトークンを入力する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/acf4ce7edb7c4bdfaddbd2a8e9cbdb41.png)