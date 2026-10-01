---
title: プリザンターからAWS SESでメールを送信できるように設定する
category: 追加設定：通知
order: '130'
status: ''
parts: ''
urlstring: mail-aws-ses
translationKey: mail-aws-ses
shortname: ''
created: 2026-05-26
updated: 2026-06-09
---

## 概要

プリザンターのリマインダーや通知機能でメールを送信するために、Amazon SES（Simple Email Service）V2 REST APIを使ったメール送信の設定方法を説明します。AWS Signature V4による認証を使用するため、AWS SDKのインストールは不要です。

## 注意事項

1. [Mail.json](../../parameters/mail-json.md)のパラメータ変更時は「[パラメータ変更時の確認事項](../../parameters/parameter-edit.md)」をご確認ください。
1. セキュリティ上の理由から、AWSの認証情報は「Mail.json」に直接記述せず、環境変数で設定することを推奨します。詳細は「操作手順2.環境変数による設定（推奨）」を参照してください。
1. 一時クレデンシャル（AssumeRole / IAM Role）には有効期限があります。EC2・ECS・Lambda等でIAMロールを利用する場合は、環境変数経由で動的に取得した値を設定してください。
1. 「Mail.json」の設定変更後はプリザンターの再起動が必要です。再起動を行うまで変更は反映されません。

## 前提条件

1. 有効なAWSアカウントが必要です。
1. 使用するリージョンでAmazon SESが有効化されていること。
1. 送信元として使用するメールアドレスまたはドメインがSESで検証済みであること。
1. SESへの送信権限を持つIAM認証情報を用意してください。使用する認証方式に応じて、以下のいずれかを選択します。  
   **方式①：IAMユーザーの永続キー**…AccessKeyIdとSecretAccessKeyが必要です。  
   **方式②：一時クレデンシャル（AssumeRole・IAM Role）**…AccessKeyId、SecretAccessKey、SessionTokenの3つが必要です。
1. IAMユーザーまたはロールに、以下のポリシーが付与されていること。

       ```json
       {
           "Version": "2012-10-17",
           "Statement": [
               {
                   "Effect": "Allow",
                   "Action": [
                       "ses:SendEmail",
                       "ses:SendRawEmail"
                   ],
                   "Resource": "*"
               }
           ]
       }
       ```

1. （推奨）SESサンドボックスを解除し、本番アクセスをリクエスト済みであること。サンドボックスモードでは、検証済みアドレスにのみ送信可能です。

## 操作手順

### 1. Mail.jsonの設定

設定ファイル[Mail.json](../../parameters/mail-json.md)を編集し、ProviderにAwsSesを指定してください。また、AwsSesセクションに認証情報とリージョンを設定してください。

#### 方式①：IAMユーザーの永続キーを使用する場合

```json
{
    "Provider": "AwsSes",
    "AwsSes": {
        "AccessKeyId": "YOUR_AWS_ACCESS_KEY_ID",
        "SecretAccessKey": "YOUR_AWS_SECRET_ACCESS_KEY",
        "SessionToken": null,
        "Region": "ap-northeast-1",
        "ConfigurationSetName": null
    },
    "FixedFrom": "noreply@example.com",
    "SupportFrom": "\"Support\" <support@example.com>"
}
```

#### 方式②：一時クレデンシャル（AssumeRole・IAM Role）を使用する場合

```json
{
    "Provider": "AwsSes",
    "AwsSes": {
        "AccessKeyId": "YOUR_AWS_ACCESS_KEY_ID",
        "SecretAccessKey": "YOUR_AWS_SECRET_ACCESS_KEY",
        "SessionToken": "YOUR_AWS_SESSION_TOKEN",
        "Region": "ap-northeast-1",
        "ConfigurationSetName": null
    },
    "FixedFrom": "noreply@example.com",
    "SupportFrom": "\"Support\" <support@example.com>"
}
```

#### 設定項目の説明

| パラメータ                  | 設定例                                | 説明                                                                                                                                         |
| :-------------------------- | :------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------- |
| Provider                    | "AwsSes"                              | AWS SESを使用する場合はAwsSesを指定します。                                                                                                  |
| AwsSes.AccessKeyId          | "YOUR_AWS_ACCESS_KEY_ID"            | AWSアクセスキーIDを指定します。システム環境変数への登録を推奨します。                                                                        |
| AwsSes.SecretAccessKey      | "YOUR_AWS_SECRET_ACCESS_KEY"        | AWSシークレットアクセスキーを指定します。システム環境変数への登録を推奨します。                                                              |
| AwsSes.SessionToken         | "YOUR_AWS_SESSION_TOKEN"            | 一時クレデンシャル（方式2）を使用する場合のみ指定します。永続キー（方式1）を使用する場合はnullを指定。システム環境変数への登録を推奨します。 |
| AwsSes.Region               | "ap-northeast-1"                      | 使用するAWSリージョンを指定します。                                                                                                          |
| AwsSes.ConfigurationSetName | null                                  | SESのConfiguration Set名を指定します。メトリクス追跡が不要な場合はnullを指定。                                                               |
| FixedFrom                   | "noreply@example.com"                 | メール送信時のfromアドレスを指定します。                                                                                                     |
| SupportFrom                 | "\"Support\" \<support@example.com\>" | サポート用メールアドレスを指定します。                                                                                                       |

各パラメータの詳細については[Mail.json](../../parameters/mail-json.md)を参照してください。

### 2.環境変数による設定（推奨）

AWSの認証情報は、[Mail.json](../../parameters/mail-json.md)の代わりに環境変数で設定できます。[Mail.json](../../parameters/mail-json.md)に値が設定されている場合はそちらが優先されます。

プリザンターは[Mail.json](../../parameters/mail-json.md)の値が空（""）またはnullの場合にのみ、環境変数から取得します。

#### 対応する環境変数

| 対象パラメータ         | 環境変数名（EnvironmentName形式）             | 環境変数名（ServiceName形式）             |
| :--------------------- | :-------------------------------------------- | :---------------------------------------- |
| AwsSes.AccessKeyId     | {EnvironmentName}_Mail_AwsSes_AccessKeyId     | {ServiceName}_Mail_AwsSes_AccessKeyId     |
| AwsSes.SecretAccessKey | {EnvironmentName}_Mail_AwsSes_SecretAccessKey | {ServiceName}_Mail_AwsSes_SecretAccessKey |
| AwsSes.SessionToken    | {EnvironmentName}_Mail_AwsSes_SessionToken    | {ServiceName}_Mail_AwsSes_SessionToken    |

{EnvironmentName}と{ServiceName}は[Service.json](../../parameters/service-json.md)の設定値に対応します。デフォルトのServiceNameはPleasanterです。

#### PowerShell（Windows）での設定方法

```powershell
$env:Pleasanter_Mail_AwsSes_AccessKeyId = "YOUR_AWS_ACCESS_KEY_ID"
$env:Pleasanter_Mail_AwsSes_SecretAccessKey = "YOUR_AWS_SECRET_ACCESS_KEY"
# 一時クレデンシャル（方式2）使用時のみ
$env:Pleasanter_Mail_AwsSes_SessionToken = "YOUR_AWS_SESSION_TOKEN"
```

#### bash（LinuxまたはmacOS）での設定方法

```bash
export Pleasanter_Mail_AwsSes_AccessKeyId="YOUR_AWS_ACCESS_KEY_ID"
export Pleasanter_Mail_AwsSes_SecretAccessKey="YOUR_AWS_SECRET_ACCESS_KEY"
# 一時クレデンシャル（方式2）使用時のみ
export Pleasanter_Mail_AwsSes_SessionToken="YOUR_AWS_SESSION_TOKEN"
```

### 3. プリザンターの再起動

設定変更を反映するため、プリザンターを再起動してください。

Windows環境の場合、IISを再起動してください。

Linux環境の場合、以下のコマンドでサービスを再起動してください。

```bash
sudo systemctl restart pleasanter
```

Microsoft Azure環境の場合、App Serviceを再起動してください。

## 対応バージョン

| 対応バージョン | 内容                                         |
| :------------- | :------------------------------------------- |
| 1.5.5.0以降    | Amazon SES V2 REST APIによるメール送信に対応 |
