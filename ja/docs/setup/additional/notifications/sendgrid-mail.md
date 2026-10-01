---
title: プリザンターからSendGridでメールを送信できるように設定する
category: 追加設定：通知
order: '110'
status: ''
parts: ''
urlstring: sendgrid-mail
translationKey: sendgrid-mail
shortname: ''
created: 2026-05-26
updated: 2026-06-09
---

## 概要

プリザンターのリマインダーや通知機能でメールを送信するために、SendGrid Web APIを使ったメール送信の設定方法を説明します。

## 注意事項

1. <span class="pl-attention">**バージョン1.5.5.0以降、Providerパラメータの追加に伴い設定方式が変更されています。既存環境からの移行については[メール送信プロバイダー設定の移行について](mail-provider-migration.md)を参照してください。**</span>
1. パラメータ変更時は「[パラメータ変更時の確認事項](../../parameters/parameter-edit.md)」をご確認ください。
1. セキュリティ上の理由から、APIキーは[Mail.json](../../parameters/mail-json.md)に直接記述せず、環境変数で設定することを推奨します。詳細は「操作手順2.環境変数による設定（推奨）」を参照してください。
1. 「Mail.json」の設定変更後はプリザンターの再起動が必要です。再起動を行うまで変更は反映されません。

## 前提条件

1. SendGridのAPIキーを用意してください。
1. 送信元として使用するメールアドレスまたはドメインが、SendGridで送信者認証（Sender Authentication）済みであることを確認してください。

## 操作手順

### 1. Mail.jsonの設定

設定ファイル[Mail.json](../../parameters/mail-json.md)を編集し、ProviderにSendGridを指定してください。また、SendGridセクションのApiKeyにSendGridのAPIキーを設定してください。

```json
{
    "Provider": "SendGrid",
    "SendGrid": {
        "ApiKey": "SG.xxxxAPIキーxxxxxx..."
    },
    "FixedFrom": "noreply@example.com",
    "SupportFrom": "\"Support\" <support@example.com>"
}
```

#### 設定項目の説明

| パラメータ      | 設定例                                | 説明                                                                                          |
| :-------------- | :------------------------------------ | :-------------------------------------------------------------------------------------------- |
| Provider        | "SendGrid"                            | SendGridを使用する場合はSendGridを指定します。                                                |
| SendGrid.ApiKey | "SG.xxxxAPIキーxxxxxx..."             | SendGridのAPIキーを指定します。環境変数へ登録するには、空（""）またはnullを指定してください。 |
| FixedFrom       | "noreply@example.com"                 | メール送信時のfromアドレスを指定します。                                                      |
| SupportFrom     | "\"Support\" \<support@example.com\>" | サポート用メールアドレスを指定します。                                                        |

各パラメータの詳細は[Mail.json](../../parameters/mail-json.md)を参照してください。

### 2.環境変数による設定（推奨）

SendGridのAPIキーは、Mail.jsonの代わりに環境変数へ登録できます。[Mail.json](../../parameters/mail-json.md)で値を指定している場合は、そちらが優先されます。

プリザンターは[Mail.json](../../parameters/mail-json.md)の値が空（""）またはnullの場合にのみ、環境変数から取得します。

#### 対応する環境変数

| 対象パラメータ  | 環境変数名（EnvironmentName形式）      | 環境変数名（ServiceName形式）      |
| :-------------- | :------------------------------------- | :--------------------------------- |
| SendGrid.ApiKey | {EnvironmentName}_Mail_SendGrid_ApiKey | {ServiceName}_Mail_SendGrid_ApiKey |

{EnvironmentName}と{ServiceName}は[Service.json](../../parameters/service-json.md)のパラメータEnvironmentName、ServiceNameの各設定値に対応します。デフォルトのServiceNameはPleasanterです。

#### PowerShell（Windows）での設定方法

```ps1
$env:Pleasanter_Mail_SendGrid_ApiKey = "SG.xxxxAPIキーxxxxxx..."
```

#### bash（LinuxまたはmacOS）での設定方法

```bash
export Pleasanter_Mail_SendGrid_ApiKey="SG.xxxxAPIキーxxxxxx..."
```

### 3. プリザンターの再起動

設定変更を反映するため、プリザンターを再起動してください。

Windows環境の場合は、IISを再起動してください。

Linux環境の場合は、以下のコマンドでサービスを再起動してください。

```bash
sudo systemctl restart pleasanter
```

Microsoft Azure環境の場合は、App Serviceを再起動してください。

## 対応バージョン

| 対応バージョン | 内容                                               |
| :------------- | :------------------------------------------------- |
| 1.3.18.0以降   | SendGridによるメール送信に対応（SmtpHost指定方式） |
| 1.5.5.0以降    | 以下のパラメータを追加<br>・Provider<br>・ApiKey   |

## 関連情報

-   [メール送信プロバイダー設定の移行について](mail-provider-migration.md)