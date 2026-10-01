---
title: 通知
category: 通知
order: '0'
status: ''
parts: ''
urlstring: table-management-notification
translationKey: table-management-notification
shortname: 通知
created: 2019-12-05
updated: 2026-02-12
---

## 概要

期限付きテーブルなどでレコードの新規作成や更新、削除などの操作を行った際に、メールまたはTeamsやSlack、Chatworkなどのコミュニケーションツールに自動通知する機能です。[ビュー](../../../users-guide/table/record-authoring/data-analysis/table-record-view.md)と組み合わせることで、通知の条件を指定することができます。

## 事前準備

- 利用する通知種別は、「パラメータ設定：Notification.json」で有効化しておきます。
- この操作を実行するユーザは、サイトの管理権限が必要です。

## 操作手順

通知機能の設定画面を呼び出すには、次のように操作します。

1. 通知機能を設定したいテーブルを開きます。
1. ナビゲーションメニューで「管理」-[テーブルの管理](../index.md)をクリックします。
1. [通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブをクリックします。

![テーブルの管理の「通知」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/notifications/assets/e4ef72faa24c49759a21e531b1444683.png)

## 設定項目

|項目名|説明|設定方法|
|:---|:---|:---|
|ID|通知の管理ID|編集不可|
|通知種別|通知の種別を指定|メール、Slack、ChatWork、LINE、LINEグループ、LINE WORKS、Teams、Rocket.Chat、InCircle、HTTPクライアントから選択|
|プレフィックス|通知のタイトルの先頭に付加する文言|任意の文言を入力|
|件名|通知のタイトルに記載する文言|任意の文言を入力。未入力時はシステム固定の文言|
|アドレス|通知先を指定|任意のメールアドレス、WebHook、roomIDのURL、LINEのUserID、GroupID、またはLINE WORKSのWebhook URLを入力|
|Cc|通知メールのCcに設定するアドレスを指定|任意のメールアドレスを入力。通知種別がメールの場合のみ指定可能。|
|Bcc|通知メールのBccに設定するアドレスを指定|任意のメールアドレスを入力。通知種別がメールの場合のみ指定可能。|
|トークン※1|chatworkのトークンまたは、LINEボットアカウントのアクセストークンを指定|取得したchatworkのトークンまたはLINEボットアカウントのアクセストークンを入力|
|カスタムデザインを使用|カスタムデザインの使用を指定|カスタムデザインを使用する場合はチェックON|
|書式※2|通知の本文に出力する書式|本マニュアルで後述|
|変更前の条件※2|変更前の条件として指定するビューを指定|任意のビューを指定|
|論理式※3|変更前後の条件を指定|And、Orから選択|
|変更後の条件※3|変更後の条件として指定するビューを指定|任意のビューを指定|
|通知タイミング|通知タイミングを指定|本マニュアルで後述|
|変更を監視する項目※4|レコードの更新が発生した場合に変更を監視する項目を指定|任意の項目を有効化/無効化|

※1.ChatWork、LINE、LINEグループ、InCircleを指定した場合に表示されます。  
※2.「カスタムデザインを使用する」がチェックONの場合に表示されます。  
※3.ビューを設定している場合に表示されます。  
※4.通知タイミングが「更新後」の場合のみに利用します。

## 通知設定を新規作成する

1. 通知タブで「新規作成」ボタンをクリックします。
1. 通知種別(メール、Slackなど)を選択します。
1. 必要な項目を設定します。
1. 「追加」ボタンをクリックします。
1. 管理画面の「更新」ボタンをクリックします。

![通知を新規作成する詳細設定の画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/notifications/assets/8f6dd59a127947d0b9e5a4ea728ecce7.png)

## 通知設定を変更する

1. 通知設定の一覧で、該当の設定をクリックします。
1. 必要な項目を変更します。
1. 「変更」ボタンをクリックします。
1. 管理画面の「更新」ボタンをクリックします。

![登録済みの通知を変更する詳細設定の画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/notifications/assets/4b88cb2146bb4e37b22e1224b2919ea0.png)

## 通知の件名を指定する

件名には、次の文字例を記載することで指定の情報を挿入できます。

|記載する文字列|挿入される情報|
|:---|:---|
|"[項目名]"|項目の値|
|"[NotificationTrigger]"|ユーザが行った操作の文字列(作成/更新/削除)|

例：件名に "[NotificationTrigger]通知 - 【[状況]】[タイトル]" を設定

- レコード作成時："作成通知 -【未着手】レコードのタイトル"
- レコード削除時："削除通知 -【未着手】レコードのタイトル"

※ 件名の設定は、作成・更新・削除・コピーの場合のみ有効となります。
※ 未設定の場合は、作成・更新・削除時の成功メッセージと同じ文字列を表示します（「〇〇を作成しました。」等）

## メール通知の宛先を動的に設定する

下記のページをご覧ください。

[テーブルの管理：通知 - メール通知の宛先を動的に設定する](table-management-notification-routing.md)

## 通知種別を指定する

|通知種別|説明|
|:--|:--|
|メール|[プリザンターからメールを送信できるように設定する](../../../setup/additional/notifications/smtp-mail.md)|
|Slack|[Slackに通知できるように設定する](../../../setup/additional/notifications/slack.md)|
|ChatWork|[Chatworkに通知できるように設定する](../../../setup/additional/notifications/chatwork.md)|
|LINE|[LINEに通知できるように設定する（個々のユーザーに対して通知を行う場合）](../../../setup/additional/notifications/line.md)|
|LINEグループ|[LINEに通知できるように設定する（LINEグループに対して通知を行う場合）](../../../setup/additional/notifications/line.md)|
|LINE WORKS|[LINE WORKSに通知できるように設定する](../../../setup/additional/notifications/lineworks.md)
|Teams|[Microsoft Teamsに通知できるように設定する](../../../setup/additional/notifications/teams.md)|
|Rocket.Chat|[Rocket.Chatに通知できるように設定する](../../../setup/additional/notifications/rocketchat.md)|
|InCircle|[InCircleに通知できるように設定する](../../../setup/additional/notifications/incircle.md)|
|HTTPクライアント|[HttpClientで任意のURLにリクエストを送る](../../../setup/additional/notifications/httpclient.md)|

※ 選択できるのは、通知種別のうち「パラメータ設定：Notification.json」で有効化したものです。
※ メールで通知する場合はメール送信の設定が必要です。  

## 通知のタイミングを指定する

通知するタイミングを指定します。設定画面にあるチェックボックスをそれぞれオンにしたタイミングで通知されます。    

|通知タイミング|説明|通知件名の例|
|---|---|---|
|作成後|編集画面でレコードを新規作成後に通知されます。|" [タイトル] " を作成しました。|
|更新後|編集画面でレコードを更新後に通知されます。|" [タイトル] " を更新しました。|
|削除後|編集画面でレコードを削除後に通知されます。|" [タイトル] " を削除しました。|
|コピー後|編集画面でレコードをコピー後に通知されます。|" [タイトル] " を作成しました。|
|一括更新後|一覧画面でレコードを一括更新後に通知されます。|[テーブル名]: ○ 件 一括更新しました。|
|一括削除後|一覧画面でレコードを一括削除後に通知されます。|[テーブル名]: ○ 件 一括削除しました。|
|インポート後|一覧画面でレコードをインポート後に通知されます。|[テーブル名]: ○ 件追加し、○ 件更新しました。|
|無効|対象の通知設定が無効化され、通知は行われません。|-|

## 通知メッセージの本文を指定する

下記のページをご覧ください。

[テーブルの管理：通知 - メッセージ本文](table-management-notification-messagebody.md)

## 制限事項

- 一括更新・インポートによる通知の場合、固定のメールアドレスにのみ通知可能です。[RelatedUsers]や[担当者]などは使用できません。
- 件名の設定は、作成・更新・削除・コピーの場合のみ有効となります。
- HTML形式でメールを送信することはできません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.26.0 以降|作成後／更新後／削除後の通知タイミングを追加|
|1.3.2.0 以降|コピー後／一括更新後／一括削除後の通知タイミングを追加|
|1.3.3.0 以降|インポート後の通知タイミングを追加|
|1.3.9.0 以降|ユーザ/組織/グループでの動的な宛先指定としてアドレスに分類項目を指定する機能を追加|
|1.3.10.0 以降|ユーザ/組織/グループでの動的な宛先指定としてアドレスにIDを直接指定する機能を追加|
|1.3.17.0 以降|HTTPクライアントを利用した通知機能を追加|
|1.4.8.0 以降|DiffMatchPatch形式で値の差分を表示する機能を追加|
|1.4.10.0 以降|メールの宛先にCc、Bccを追加|
|1.5.1.0 以降|通知種別にLINE WORKSを追加|

## 関連情報

-   [テーブル機能：レコードのビューの切り替え](../../../users-guide/table/record-authoring/data-analysis/table-record-view.md)
-   [テーブルの管理](../index.md)
-   [応用編：通知、リマインダー](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)
-   [テーブルの管理：通知 - メール通知の宛先を動的に設定する](table-management-notification-routing.md)
-   [プリザンターからメールを送信できるように設定する](../../../setup/additional/notifications/smtp-mail.md)
-   [Slackに通知できるように設定する](../../../setup/additional/notifications/slack.md)
-   [Chatworkに通知できるように設定する](../../../setup/additional/notifications/chatwork.md)
-   [LINEに通知できるように設定する](../../../setup/additional/notifications/line.md)
-   [LINE WORKSに通知できるように設定する](../../../setup/additional/notifications/lineworks.md)
-   [Microsoft Teamsに通知できるように設定する](../../../setup/additional/notifications/teams.md)
-   [Rocket.Chatに通知できるように設定する](../../../setup/additional/notifications/rocketchat.md)
-   [InCircleに通知できるように設定する](../../../setup/additional/notifications/incircle.md)
-   [HTTPクライアントで通知できるように設定する](../../../setup/additional/notifications/httpclient.md)
-   [テーブルの管理：通知 - メッセージ本文](table-management-notification-messagebody.md)
