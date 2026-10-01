---
title: Microsoft Teamsに通知できるように設定する
category: 追加設定：通知
order: '610'
status: ''
parts: ''
urlstring: teams
translationKey: teams
shortname: ''
created: 2019-04-30
updated: 2026-06-25
---

# Teams通知に関するご案内

Microsoft側の仕様変更により、2024年8月15日以降は本手順では設定できなくなります。また本手順で既にTeams通知を行っている場合は2025年12月までは引き続き機能しますが、そのためには2024年12月31日までに追加設定が必要になります。
代替手順を準備しましたので、Teams通知をご利用のお客様は設定の見直しを行ってください。
[Microsoft Teamsに通知できるように設定する（Workflowsを利用）](teams-workflows.md)

本件における仕様変更の内容については「Microsoft Developer Blogs（英語）」の以下URLを参照してください。  
https://devblogs.microsoft.com/microsoft365dev/retirement-of-office-365-connectors-within-microsoft-teams/

---

## 前提条件

Microsoft Teams アプリにてチームおよび通知用のチャネルを作成しておきます。  
[チャネルを作成する](https://support.microsoft.com/ja-jp/office/%E3%83%81%E3%83%A3%E3%83%8D%E3%83%AB%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B-4fe74e73-e12d-4c67-8cba-d06ce8e48c24)

## Incoming Webhook コネクタの追加とURLの取得

通知用のチャネルにコネクタ「Incoming Webhook」を追加します。  

- チャネル横の「...」アイコンをクリックします。
- 「コネクタ」をクリックします。
- チャネルのコネクタ画面で「Incoming Webhook」コネクタの「構成」をクリックします。

![Teamsのチャネルのコネクタ画面。「Incoming Webhook」の「構成」を選ぶ](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/9008f726287f4170825240a8fa0ab79f.png)

- コネクタの名前を入力して「作成」をクリック後、以下の画面でURLをコピーします。

![Incoming Webhookコネクタの画面。発行されたURLをコピーする](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/a946a99d738346dc93793ea9f28d5f4a.png)

## プリザンターの設定

1.通知を設定するテーブルを選択し、[テーブルの管理](../../../managers-guide/manage-table/index.md)-[通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブを開き、「新規作成」ボタンをクリックしてください。

![テーブルの管理の「通知」タブ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/4dadd2827bf04de994a95829b97fcac6.png)

2.通知種別で「Microsoft Teams」を選択し、アドレス欄にIncoming Webhookコネクタの追加時にコピーしたURLを張り付け、[追加] ボタンをクリックしてください。

![通知の設定画面。通知種別「Microsoft Teams」でアドレスにURLを貼り付ける](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/89a30e08ebc245eea093c7a5b0bc8343.png)

3.「更新」ボタンをクリックしてください。以上で本手順は完了です。

![テーブルの管理画面。「更新」ボタンで設定を保存する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/0003c9f627be4e9eb5e5c654eeb4c038.png)
