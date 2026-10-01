---
title: メール送信できない
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-mail-smtp-troubleshooting
translationKey: faq-mail-smtp-troubleshooting
shortname: ''
created: 2026-06-19
updated: 2026-07-14
---

## 回答

バージョン1.5.6.0以降を使用し、下記を参考に[Mail.json](../../setup/parameters/mail-json.md)の各パラメータを設定してください。

---

## 概要

以下のような事象によってメール送信を行えない場合は、バージョン1.5.6.0以降で利用できる[Mail.json](../../setup/parameters/mail-json.md)の各パラメータを適切に設定してください。

| No. | 事象                                               | 設定すべきパラメータ           |
| --: | :------------------------------------------------- | :----------------------------- |
|   1 | SSL証明書の失効チェックでエラーになる              | SmtpCheckCertificateRevocation |
|   2 | 特定のTLSバージョンを強制したい                    | SmtpSslProtocols               |
|   3 | SMTP接続がタイムアウトする（デフォルト値が不適切） | SmtpTimeout                    |
|   4 | HELOコマンドのドメイン名を指定したい               | SmtpLocalDomain                |
|   5 | TLS必須環境でSTARTTLSのダウングレードを防ぎたい    | SmtpRequireTls                 |
|   6 | 送信元IPアドレスを明示的に指定したい               | SmtpLocalEndPoint              |
|   7 | プロキシ経由でSMTPサーバに接続する必要がある       | SmtpProxy*系の各パラメータ     |
|   8 | クライアント証明書認証が必要                       | SmtpClientCertificate          |

## 1. SSL証明書の失効チェックでエラーになる

[Mail.json](../../setup/parameters/mail-json.md)のSmtpCheckCertificateRevocationをfalseに設定し、証明書の失効確認をスキップしてください。<br>&nbsp;

```json
{
    "SmtpCheckCertificateRevocation": false
}
```

## 2. 特定のTLSバージョンを強制したい

[Mail.json](../../setup/parameters/mail-json.md)のSmtpSslProtocolsに強制したいTLSのバージョンを指定してください。

```json
{
    "SmtpCheckCertificateRevocation": true,
    "SmtpSslProtocols": "Tls12, Tls13",
    "SmtpTimeout": 120000
}
```

## 3. SMTP接続がタイムアウトする（デフォルト値が不適切）

[Mail.json](../../setup/parameters/mail-json.md)のSmtpTimeoutに、通信環境に応じたタイムアウト時間（単位：ms）を指定してください。

```json
{
    "SmtpTimeout": 300000
}
```

## 4. HELOコマンドのドメイン名を指定したい

[Mail.json](../../setup/parameters/mail-json.md)のSmtpLocalDomainに、SMTPクライアントとして使用するローカルドメイン名を指定してください。

```json
{
    "SmtpLocalDomain": "mail.example.com"
}
```

## 5. TLS必須環境でSTARTTLSのダウングレードを防ぎたい

[Mail.json](../../setup/parameters/mail-json.md)のSmtpRequireTlsをtrueに設定し、REQUIRETLS拡張を有効にしてください。

```json
{
    "SmtpRequireTls": true
}
```

## 6. 送信元IPアドレスを明示的に指定したい

[Mail.json](../../setup/parameters/mail-json.md)のSmtpLocalEndPointに、接続元として使用するローカルエンドポイントを"IPアドレス:ポート番号"形式で指定してください。

```json
{
    "SmtpLocalEndPoint": "192.168.1.10:0"
}
```

## 7. プロキシ経由でSMTPサーバに接続する必要がある

以下の各パラメータを設定し、HTTPSプロキシ経由で送信するように構成してください。以下の設定例では明示的に指定していますが、セキュリティの観点からSmtpProxyUserNameとSmtpProxyPasswordは環境変数で設定することを推奨します。詳細は[Mail.json](../../setup/parameters/mail-json.md)を参照してください。

```json
{
    "SmtpProxyType": "Https",
    "SmtpProxyHost": "proxy.example.com",
    "SmtpProxyPort": 443,
    "SmtpProxyUserName": "proxy-user",
    "SmtpProxyPassword": "secret",
    "SmtpProxyCheckCertificateRevocation": true,
    "SmtpProxySslProtocols": "Tls12, Tls13"
}
```

## 8. クライアント証明書認証が必要

[Mail.json](../../setup/parameters/mail-json.md)のSmtpClientCertificateにクライアント証明書を表すパラメータを指定してください。<br>&nbsp;

```json
{
    "SmtpClientCertificate": {
        "StoreName": "My",
        "StoreLocation": "CurrentUser",
        "X509FindType": "FindByThumbprint",
        "FindValue": "ABCD1234..."
    }
}
```
