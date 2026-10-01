---
title: リマインダー
category: リマインダー
order: '0'
status: ''
parts: ''
urlstring: table-management-reminder
translationKey: table-management-reminder
shortname: リマインダー
created: 2019-12-05
updated: 2026-02-12
---

## 概要

リマインダーは、期日が過ぎたレコードまたは指定範囲内で期日が近付いたレコードに対して、指定した時刻・周期でリマインド通知する機能です。リマインド通知には、メールまたはTeamsやSlack、Chatworkなどのコミュニケーションツールを利用できます。

## 前提条件

1. リマインダーを利用するには、あらかじめ[プリザンターのリマインダー機能を有効化する](../../../setup/additional/notifications/reminder.md)を実行しておきます。
1. この操作を実行するユーザは、サイトの管理権限が必要です。

## 操作手順

リマインダー機能の設定画面を呼び出すには、次のように操作します。

1. リマインダー機能を設定したいテーブルを開きます。
1. ナビゲーションメニューで「管理」-[テーブルの管理](../index.md)をクリックします。
1. [リマインダー](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブをクリックします。

![テーブルの管理の「リマインダー」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/reminders/assets/6a897dc498894105b0f83152b17d0cd7.png)

### リマインダー設定を新規作成する

1. リマインダータブで「新規作成」ボタンをクリックします。
1. リマインダー種別(メール、Slackなど)を選択します。
1. 必要な項目を設定します。
1. 「追加」ボタンをクリックします。
1. 管理画面の「更新」ボタンをクリックします。

![リマインダーを新規作成する設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/reminders/assets/b73e104759a0413bbfffdcb3d0a04b95.png)

![リマインダーの設定項目を入力した例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/reminders/assets/e44078c5bf6b4df38e756e3f12569ca4.png)

### リマインダーの発信条件

1. リマインダー機能は、"開始日時"を時刻、日、週/曜日、月の基準時点として実行します。
1. 実行したタイミングから"範囲"の日数内に指定の日付が含まれる場合、リマインドを発信します。
1. リマインドの基準とする日付項目は、設定項目の"項目"欄で指定します。
1. 各レコードの[項目](../editor/editor-settings/columns/index.md)で指定した日付と[状況](../editor/editor-settings/columns/table-management-status.md)の値で判定して送信されます。
1. [状況](../editor/editor-settings/columns/table-management-status.md)が「完了」「保留」(コードが900以上)の場合、リマインドは送信されません。
1. ただし「過去に完了したものも送信」がオンの場合は送信されます。

### 設定項目

|項目名|説明|設定方法|
|:---|:---|:---|
|リマインダー種別|リマインダーの種別を指定|メール、Slack、ChatWork、LINE、LINEグループ、LINE WORKS、Teams、Rocket.Chat、InCircleから選択|
|件名|リマインドメールの件名|任意の件名を入力|
|内容|レコード一覧の前後に文章の追加|任意の内容を入力、[Records]の位置にレコード一覧が出力される|
|行|レコード一覧に表示する項目のレイアウト|任意の内容を入力|
|差出人|メールのFROMに利用するアドレス。[Mail.json](../../../setup/parameters/mail-json.md)のFixedFromを設定している場合は、この項目は非表示となり、FixedFromで指定したアドレスが差出人となる|任意のアドレスを入力|
|宛先|メールのTOに利用するアドレス|任意のアドレスをカンマ区切りで入力|
|項目|リマインドの基準とする日付項目|任意の日付項目を指定|
|開始日時|リマインドを開始する日時|任意の日時を入力|
|期間種別|繰り返し期間の指定|毎日、毎週、週/曜日、毎月、月末、毎年から ※下記を参照|
|範囲|リマインドを行う期間。10を指定した場合、当日を含めた10日間の範囲を対象とする。例としては1日にリマインドメールが送られる場合には10日までのレコードが対象となります。|任意の日数を入力|
|過去に完了したものも送信|日付が過去で完了したものも送信するか選択|完了したものも送信する場合はチェック|
|該当がない場合は送信しない|対象レコードがない際にリマインドメールを送信しない場合はチェック|　|
|URLを送信しない|メールにURLを記載しない|メールにURLを記載しない場合はチェック|
|期限切れを送信しない|期限が過ぎているものを送信しない|期限が過ぎているものを送信しない場合はチェック|
|条件|リマインドメールを送信する条件|任意のビューを指定|
|無効|対象のリマインドを無効化|無効化する場合はチェック|

### リマインダー種別を指定する

|リマインダー種別|説明|
|:--|:--|
|メール|[プリザンターからメールを送信できるように設定する](../../../setup/additional/notifications/smtp-mail.md)|
|Slack|[Slackに通知できるように設定する](../../../setup/additional/notifications/slack.md)|
|ChatWork|[Chatworkに通知できるように設定する](../../../setup/additional/notifications/chatwork.md)|
|LINE|[LINEに通知できるように設定する（個々のユーザーに対して通知を行う場合）](../../../setup/additional/notifications/line.md)|
|LINEグループ|[LINEに通知できるように設定する（LINEグループに対して通知を行う場合）](../../../setup/additional/notifications/line.md)|
|LINE WORKS|[LINE WORKSに通知できるように設定する](../../../setup/additional/notifications/lineworks.md)|
|Teams|[Microsoft Teamsに通知できるように設定する](../../../setup/additional/notifications/teams.md)|
|Rocket.Chat|[Rocket.Chatに通知できるように設定する](../../../setup/additional/notifications/rocketchat.md)|
|InCircle|[InCircleに通知できるように設定する](../../../setup/additional/notifications/incircle.md)|

※ 選択できるのは、リマインダー種別のうち「パラメータ設定：Reminder.json」で有効化したものです。 
※ メールで通知する場合はメール送信の設定が必要です。  

### 期間種別を指定する

|期間種別|説明|
|:--|:--|
|毎日|毎日、開始日時に指定した同時刻に実行  |
|毎週|週に1回、開始日時に指定した曜日の同時刻に実行  |
|週/曜日|月に1回、開始日時に指定した第〇週の〇曜日の同時刻に実行 |
|毎月|月に1回、開始日時に指定した日の同時刻に実行 |
|月末|月に1回、開始日時に指定した日の月末日の同時刻に実行  |
|毎年|年に1回、開始日時に指定した日の同時刻に実行|

## リマインダーの宛先を動的に設定する

下記のページをご覧ください。

[テーブルの管理：リマインダーの宛先を動的に設定する](table-management-reminder-routing.md)

## メールのタイトルや本文に項目の内容を出力する

宛先と同様に、タイトルと本文にも項目の内容を出力することができます。  

![タイトルと本文に項目の内容を出力したリマインダーの設定](https://pleasanter.org/files/images/ja/managers-guide/manage-table/reminders/assets/302179a7b1e84beca36b0447d5f013da.png)

## 制限事項

- リマインダーメールのFROMはFixedFromで設定したメールアドレスとなります。
- [Mail.json](../../../setup/parameters/mail-json.md)のFixedFromを設定している場合、差出人の入力項目は非表示となります。
- HTML形式でメールを送信することはできません。
- リマインダーで送付されるレコード一覧のソート順は、項目で指定した日付項目の降順で固定となります。任意の順に変更することはできません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.9.0 以降|ユーザ/組織/グループでの動的な宛先指定としてアドレスに分類項目を指定する機能を追加|
|1.3.10.0 以降|ユーザ/組織/グループでの動的な宛先指定としてアドレスにIDを直接指定する機能を追加<br>リマインダー種別の指定機能を追加|
|1.5.1.0 以降|通知種別にLINE WORKSを追加|