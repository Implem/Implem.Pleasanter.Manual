---
title: Microsoft Teamsに通知できるように設定する（Workflowsを利用）
category: 追加設定：通知
order: '600'
status: ''
parts: ''
urlstring: teams-workflows
translationKey: teams-workflows
shortname: ''
created: 2024-07-18
updated: 2026-06-09
---

## 制限事項

1. 本手順で通知設定した場合、通知者が「Workflows 経由の●●」という表示になります。この「●●」はワークフローを作成したユーザの氏名となります。この表示内容を変更したい場合はチャットボットの導入を検討ください。
![Teamsに届いた通知。投稿者が「Workflows 経由の●●」と表示されている](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/822d2845be684c08b1c644d5265a097d.png)

## 1. 事前準備

Microsoft Teams アプリにてチームおよび通知用のチャネルを作成しておきます。  
[チャネルを作成する](https://support.microsoft.com/ja-jp/office/%E3%83%81%E3%83%A3%E3%83%8D%E3%83%AB%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B-4fe74e73-e12d-4c67-8cba-d06ce8e48c24)

## 2. ワークフローの作成とURLの取得  

通知用のチャネルにワークフローを追加します。  
1. チャネル横の「...」アイコンをクリックし、メニューより「ワークフロー」をクリックします。
![Teamsのチャネル横の「...」メニュー。「ワークフロー」を選ぶ](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/de32efd6f6f04b7d97d81567b91bbf98.png)

1. ダイアログの「その他ワークフロー」ボタンをクリックします。
![ワークフローのダイアログ。「その他ワークフロー」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/3516825cdce04f97bc9e2359b20065d0.png)

1. 「＋ 一から作成」ボタンをクリックします。
![ワークフローの作成画面。「＋ 一から作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/7c0bcb2aab564067a172793ea624bb99.png)

1. 検索欄に「webhook」と入力し、下部の検索結果から「Teams Webhook要求を受信したとき」をクリックします。
![トリガーの検索結果。「Teams Webhook要求を受信したとき」を選ぶ](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/58756d2dbd7d4080a248ad51906fe230.png)

1. 「Who Can Trigger the flow?」で「Anyone」を選択し、「新しいステップ」ボタンをクリックします。
![トリガーの設定。「Who Can Trigger the flow?」で「Anyone」を選ぶ](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/6ae4262320014905b562f14a02ecc844.png)

1. 検索欄に「teams」と入力し、下部の検索結果から「チャットまたはチャネルでメッセージを投稿する」をクリックします。
![アクションの検索結果。「チャットまたはチャネルでメッセージを投稿する」を選ぶ](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/52092bc663ea440ca77104b22e8a9266.png)

1. 各項目を入力し、「保存」をクリックします。

    |入力項目|内容|
    |:---|:---|
    |投稿者|「フローボット」を選択|
    |投稿先|「Channel」を選択|
    |Team|1. 事前準備で作成したチームを選択|
    |Channel|1. 事前準備で作成した通知用チャネルを選択|
    |Message|以下文字列をコピー＆ペースト<br>@{triggerBody()?['text']}|

    ![メッセージ投稿アクションの設定画面。投稿者や投稿先などを入力する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/69b0c24ecd31475090090316ba33692c.png)

1. 「When a Teams webhook request is received」をクリックし、「HTTP POST のURL」欄右の「URLのコピー」ボタンをクリックします。
![トリガーの画面。「HTTP POST のURL」の「URLのコピー」ボタン](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/39445a9b30324b159c1a6835b2e5bae6.png)

## 3. プリザンターの設定

1.通知を設定するテーブルを選択し、[テーブルの管理](../../../managers-guide/manage-table/index.md)-[通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブを開き、「新規作成」ボタンをクリックしてください。
![テーブルの管理の「通知」タブ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/20e88dc282f44529b0a267f5d70d291e.png)

2.通知種別で「Teams」を選択し、アドレス欄に2.8.でコピーしたURLを張り付け、[追加] ボタンをクリックしてください。
![通知の設定画面。通知種別「Teams」でアドレスにURLを貼り付ける](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/11c8924f93f743d690255682efcbb0a5.png)

3.「更新」ボタンをクリックしてください。以上で本手順は完了です。
![テーブルの管理画面。「更新」ボタンで設定を保存する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/2a004af8fc51416c8eda9bed45714882.png)