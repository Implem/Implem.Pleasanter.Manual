---
title: 通知
category: プロセス
order: '800'
status: ''
parts: ''
urlstring: process-notification
translationKey: process-notification
shortname: ''
created: 2025-06-19
updated: 2026-02-10
---

## 概要

プロセス実行時に通知する内容を設定します。通知が実行されるのは、以下の場合です。

1.  実行種別が「作成または更新」
1.  実行種別が「追加したボタン」かつアクション種別が「保存」

## 制限事項

-   HTML形式でメールを送信することはできません。

## 事前準備

1.  利用する通知種別は、「パラメータ設定：Notification.json」で有効化しておきます。

## 操作手順

1.  通知タブをクリックします。
1.  「新規作成」ボタンをクリックします。
1.  通知種別（メール、Slackなど）を選択します。
1.  必要な項目を設定します。
1.  「変更」ボタンをクリックします。
1.  プロセス管理の「更新」ボタンをクリックします。

![プロセスの通知タブ。設定した通知が一覧表示される](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/5724b477438a4432b7f2df355a09b87d.png)

## 設定項目

![プロセスの通知の設定画面。通知種別や件名、アドレスなどを設定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/c5df842e541d44f2b9fe8a5282a2764c.png)

| 項目名   | 説明                                                                   | 設定方法                                                                                                 |
| :------- | :--------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------- |
| ID       | 通知の管理ID                                                           | 編集不可                                                                                                 |
| 通知種別 | 通知の種別を指定                                                       | メール、Slack、ChatWork、LINE、LINEグループ、LINE WORKS、Teams、Rocket.Chat、InCircleから選択            |
| 件名     | 通知するメールの件名を指定(*必須)                                      | 任意の件名を入力 ※2                                                                                      |
| アドレス | 通知先を指定(*必須)                                                    | 任意のメールアドレス、WebHook、roomIDのURL、LINEのUserID、GroupID、またはLINE WORKSのWebhook URLを入力。 |
| Cc       | 通知メールのCcに設定するアドレスを指定                                 | 任意のメールアドレスを入力。通知種別がメールの場合のみ指定可能。                                         |
| Bcc      | 通知メールのBccに設定するアドレスを指定                                | 任意のメールアドレスを入力。通知種別がメールの場合のみ指定可能。                                         |
| トークン | chatworkのトークンまたは、LINEボットアカウントのアクセストークンを指定 | 取得したchatworkのトークンまたはLINEボットアカウントのアクセストークンを入力 [^1]                        |
| 内容     | 通知の本文に出力する書式(*必須)                                        | 任意の内容を入力 [^2]                                                                                    |

[^1]: ChatWork、LINE、LINEグループ、InCircleを指定した場合に表示されます。
[^2]: 角括弧（`[ ]`）囲いで項目名を指定することで、動的にメッセージを設定することができます。

    ``` text
    申請しました。申請金額 ：[金額]
    ```

## 通知種別を指定する

| 通知種別     | 説明                                                                                                                      |
| :----------- | :------------------------------------------------------------------------------------------------------------------------ |
| メール       | [プリザンターからメールを送信できるように設定する](../../../setup/additional/notifications/smtp-mail.md)                  |
| Slack        | [Slackに通知できるように設定する](../../../setup/additional/notifications/slack.md)                                       |
| ChatWork     | [Chatworkに通知できるように設定する](../../../setup/additional/notifications/chatwork.md)                                 |
| LINE         | [LINEに通知できるように設定する（個々のユーザーに対して通知を行う場合）](../../../setup/additional/notifications/line.md) |
| LINEグループ | [LINEに通知できるように設定する（LINEグループに対して通知を行う場合）](../../../setup/additional/notifications/line.md)   |
| LINE WORKS   | [LINE WORKSに通知できるように設定する](../../../setup/additional/notifications/lineworks.md)                              |
| Teams        | [Microsoft Teamsに通知できるように設定する](../../../setup/additional/notifications/teams.md)                             |
| Rocket.Chat  | [Rocket.Chatに通知できるように設定する](../../../setup/additional/notifications/rocketchat.md)                            |
| InCircle     | [InCircleに通知できるように設定する](../../../setup/additional/notifications/incircle.md)                                 |

-   選択できるのは、通知種別のうち「パラメータ設定：Notification.json」で有効化したものです。
-   メールで通知する場合はメール送信の設定が必要です。

## メール通知の宛先に指定できる対象

| 対象                                          | 挙動                                                                                                                                                       |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 固定のメールアドレス（<example@example.com>） | 対象レコードの全てが指定した固定アドレスに送信されます。複数の固定アドレスを指定した場合には、全ての固定アドレスをTOとして送信します                       |
| 担当者、管理者                                | 対象レコードの担当者、管理者に指定されたユーザのメールアドレスに送信します                                                                                 |
| タイトル、内容、分類、説明                    | 対象レコードのタイトル、内容、分類、説明に記載されたメールアドレスすべてに送信します。メールアドレスはカンマ区切りまたは改行区切りで指定することができます |

## 対応バージョン

| 対応バージョン | 内容                                                                             |
| :------------- | :------------------------------------------------------------------------------- |
| 1.4.10.0 以降  | 変更種別に値の関数操作を追加<br>メール通知の宛先にCc、Bccを追加                  |
| 1.4.11.0 以降  | 実行種別に追加したボタン／作成・更新を追加<br>共通設定・全般タブにアイコンを追加 |
| 1.5.1.0 以降   | 通知タブの通知種別にLINE WORKSを追加                                             |

## 関連情報

-   [プリザンターからメールを送信できるように設定する](../../../setup/additional/notifications/smtp-mail.md)
-   [Slackに通知できるように設定する](../../../setup/additional/notifications/slack.md)
-   [Chatworkに通知できるように設定する](../../../setup/additional/notifications/chatwork.md)
-   [LINEに通知できるように設定する](../../../setup/additional/notifications/line.md)
-   [LINE WORKSに通知できるように設定する](../../../setup/additional/notifications/lineworks.md)
-   [Microsoft Teamsに通知できるように設定する](../../../setup/additional/notifications/teams.md)
-   [Rocket.Chatに通知できるように設定する](../../../setup/additional/notifications/rocketchat.md)
-   [InCircleに通知できるように設定する](../../../setup/additional/notifications/incircle.md)
