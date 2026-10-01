---
title: 多要素認証とパスキー認証を同時に設定した場合でのパラメータ設定について教えてください
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-mfa-passkey-parameter-settings
translationKey: faq-mfa-passkey-parameter-settings
shortname: ''
created: 2026-04-15
updated: 2026-04-15
---

## 回答

多要素認証とパスキー認証を同時に設定する場合は、設定ファイル**Authentication.jsonのパラメータUserVerificationRequirement（バージョン1.5.3.0で追加）を設定**してください（パラメータの詳細は[パスキー認証](../../setup/additional/authn-authz/passkey.md)を参照）。プリザンターの再起動後、以下の挙動となります。

![パラメータの設定値ごとの挙動をまとめた図](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/de2ea7888dfb4f8491229f84fadc051a.png)

---

## 概要

（TOTPまたはメールによる）二段階認証とパスキー認証を同時に設定するには、プリザンター1.5.3.0で追加されたAuthentication.jsonのパラメータ「UserVerificationRequirement」を設定します。

設定例は以下の通りです。

##### Authentication.json（パスキー認証の設定箇所を抜粋）

```json
{
    "PasskeyParameters": {
        "Enabled": true,
        "ServerName": "Pleasanter",
        "ServerDomain": "example.com",
        "Origins": [
            "https://example.com",
            "https://example.com:443"
        ],
        "UserVerificationRequirement": "Preferred"
    }
}
```

二段階認証とパスキー認証の両方が有効な環境では、以下の挙動となります。

1. 「パスキーでログイン」した場合、二段階認証画面は表示されません。
1. 「ログインID」と「パスワード」でログインした場合、二段階認証画面が表示されます。

## 前提条件

1. プリザンター1.5.3.0以降を使用してください。
1. 各認証方式が正しく設定されている必要があります。各認証機能の設定手順は、それぞれのマニュアルを参照してください。

   | 機能 | パラメータファイル | 参照マニュアル |
   |:--|:--|:--|
   | パスキー認証 |[Authentication.json](../../setup/parameters/authentication-json.md)| [パスキー認証](../../setup/additional/authn-authz/passkey.md) |
   | メールによる二段階認証 |[Security.json](../../setup/parameters/security-json.md)| [メールによる二段階認証を有効にする](../../setup/additional/authn-authz/secondary-authentication.md) |
   | TOTPによる二段階認証 |[Security.json](../../setup/parameters/security-json.md)| [TOTPによる二段階認証を有効にする](../../setup/additional/authn-authz/totp-authentication.md) |

## 関連情報

- [パスキー認証](../../setup/additional/authn-authz/passkey.md)
- [メールによる二段階認証を有効にする](../../setup/additional/authn-authz/secondary-authentication.md)
- [TOTP（Time-based One-Time Password）による二段階認証を有効にする](../../setup/additional/authn-authz/totp-authentication.md)
- [パラメータ設定：Authentication.json](../../setup/parameters/authentication-json.md)
- [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
- [パラメータ変更時の確認事項](../../setup/parameters/parameter-edit.md)