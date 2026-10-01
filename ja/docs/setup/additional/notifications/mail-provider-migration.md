---
title: メール送信プロバイダー設定の移行について
category: 追加設定：通知
order: '90'
status: ''
parts: ''
urlstring: mail-provider-migration
translationKey: mail-provider-migration
shortname: メール送信プロバイダー設定の移行について
created: 2026-05-26
updated: 2026-06-09
---

## 概要

バージョン1.5.5.0より、[Mail.json](../../parameters/mail-json.md)にProviderパラメータが追加され、SMTP、SendGrid、Amazon SESをメール送信プロバイダとして明示的に指定する仕様に変更になりました。

本ページでは、各プロバイダの既存環境への影響と移行手順を説明します。

## 注意事項

1. パラメータ変更時は「[パラメータ変更時の確認事項](../../parameters/parameter-edit.md)」をご確認ください。
1. [Mail.json](../../parameters/mail-json.md)の設定変更後はプリザンターの再起動が必要です。再起動を行うまで変更は反映されません。

## 操作手順

### 1. SMTPを使用中の環境

Providerのデフォルト値はSmtpです。バージョン1.5.5.0への移行後、[Mail.json](../../parameters/mail-json.md)のProviderが"Smtp"に設定されていることを確認してください。

### 2. SendGridを使用中の環境からの移行（任意）

SmtpHostにsmtp.sendgrid.netを設定していた既存環境は、バージョン1.5.5.0適用後も[Mail.json](../../parameters/mail-json.md)の設定変更は不要です。新しい設定方式への移行は任意ですが、保守の観点から移行を推奨します。

移行する場合は、以下の手順で[Mail.json](../../parameters/mail-json.md)を編集してください。

1. Providerを"SendGrid"に変更します。
2. SendGridセクションを追加し、ApiKeyにAPIキーを設定します。
3. SmtpHost、SmtpPort、SmtpUserName、SmtpPasswordの各項目を削除します（任意）。

移行後の設定例を以下に示します。

##### Mail.jsonの設定例

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

詳細な設定手順については「[プリザンターからSendGridでメールを送信できるように設定する](sendgrid-mail.md)」を参照してください。

## 対応バージョン

| 対応バージョン | 内容 |
|:--|:--|
| 1.5.5.0以降 | Providerパラメータを追加。SendGrid Web APIおよびAmazon SES V2 REST APIによるメール送信に対応。既存のSendGrid環境（SmtpHost: smtp.sendgrid.net）の後方互換性を確保 |

## 関連情報

[プリザンターからメールを送信できるように設定する](smtp-mail.md)  
[プリザンターからSendGridでメールを送信できるように設定する](sendgrid-mail.md)    
[パラメータ設定：Mail.json](../../parameters/mail-json.md)