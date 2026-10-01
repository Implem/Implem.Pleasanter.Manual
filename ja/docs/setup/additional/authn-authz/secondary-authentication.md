---
title: メールによる二段階認証を利用する
category: 追加設定：認証
order: '400'
status: ''
parts: ''
urlstring: secondary-authentication
translationKey: secondary-authentication
shortname: メールによる二段階認証
created: 2020-08-12
updated: 2026-06-16
---

## 概要

メールによる二段階認証を使用するためには、以下の設定が必要です。  

#### ①メールを送信できるように設定する  

[プリザンターからメールを送信できるように設定する](../notifications/smtp-mail.md)を参考にメールの送信設定を済ませてください。パラメータ"SupportFrom"の設定は必須です。

#### ②ユーザのメールアドレスの設定する  

[ユーザ管理機能](../../../managers-guide/user-administration/index.md)を参考に、ユーザのメールアドレスを設定してください。

#### ③Security.jsonのSecondaryAuthenticationパラメータで有効化する   

##### [Security.json](../../parameters/security-json.md)

```json
"SecondaryAuthentication": {
    "Mode": "DefaultEnable",
    "NotificationType": "Mail",
    "AuthenticationCodeCharacterType": "Number",
    "AuthenticationCodeLength": 8,
    "AuthenticationCodeExpirationPeriod": 300
}
```

## 制限事項

パスキー認証と二段階認証の両方が有効な環境では以下の挙動となります。  

1. パスキー認証でログインした場合、二段階認証画面は表示されません。  
1. ID、パスワードでログインした場合、二段階認証画面が表示されます。

## ログイン手順

1. 二段階認証を有効にしてログインすると、確認コードの入力画面に遷移します。  
   ![メールによる二段階認証の確認コード入力画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/d0a528ddbc5c45e1ae19c75b006b0b62.png)
1. ログイン処理を行ったタイミングで、ユーザ情報として登録されたメールアドレス宛に以下のようなメールが送信されます。  
   ![確認コードが記載された通知メールの例](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/11302f473567415e8df7d875838586ba.png)
1. 確認コードの有効時間内に確認コードを入力して、ログインしてください。

## 関連情報

-   [プリザンターからメールを送信できるように設定する](../notifications/smtp-mail.md)
-   [ユーザ管理機能](../../../managers-guide/user-administration/index.md)
-   [パラメータ設定：Security.json](../../parameters/security-json.md)