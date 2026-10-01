---
title: TOTP（Time-based One-Time Password）による二段階認証を利用する
category: 追加設定：認証
order: '500'
status: ''
parts: ''
urlstring: totp-authentication
translationKey: totp-authentication
shortname: TOTPによる二段階認証
created: 2024-03-06
updated: 2026-04-14
---

## 概要

TOTP認証を使用するには、以下の設定が必要です。  

#### ①Security.jsonのSecondaryAuthenticationパラメータで有効化する   

##### [Security.json](../../parameters/security-json.md)

```json
"SecondaryAuthentication": {
    "Mode": "DefaultEnable",
    "NotificationType": "Totp",
    "CountTolerances": 1,
    "NotificationMailBcc": false,
    "AuthenticationCodeCharacterType": "Number",
    "AuthenticationCodeLength": 8,
    "AuthenticationCodeExpirationPeriod": 300
},
```

#### ②認証用の端末にTOTP認証に対応したアプリケーションをインストールする

スマートフォンなど認証用の端末に、Google AuthenticatorやMicrosoft AuthenticatorなどのTOTP認証に対応している認証アプリをインストールしてください。この設定はプリザンターにログインするユーザ毎に実施が必要です。

## 制限事項

パスキー認証と二段階認証の両方が有効な環境では以下の挙動となります。  

1. パスキー認証でログインした場合、二段階認証画面は表示されません。  
1. ID、パスワードでログインした場合、二段階認証画面が表示されます。

## ログイン手順

1. TOTP認証を有効にすると、通常のID/パスワードを入力後に確認コードの入力画面へ移動します。 
1. 初回ログイン時には、下図の様にQRコードが表示されます。
   ![TOTP認証の初回ログイン時に表示される、認証アプリ連携用のQRコード](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/0c16d8abc76c4d62b8af55c06175f650.png)
1. 2回目以降は確認コードの入力欄のみが表示されます。

## （初回のみ）認証アプリでQRコードを読み取る

表示されたQRコードを認証アプリで読み取ってください。認証アプリ内に以下のような画面が表示されます（認証アプリによって表示内容が異なる場合があります）。

```csv
Implem Pleasanter      （サービス名（固定値））
hayato@implem.co.jp    （ログインID）
012 345                （確認コード）
```

## 確認コードを入力する

認証アプリに表示されている確認コードをプリザンターのログイン画面に入力し、「確認」ボタンをクリックします。問題がなければログイン完了です。

#### ①確認コードについて

1. 確認コードは30秒ごとに更新されます。更新された場合は新しいコードを再入力してください。
1. パラメータ設定：[Security.json](../../parameters/security-json.md)内のSecondaryAuthenticationパラメータのCountTolerancesを調整することで、指定した回数分古い確認コードでもログインできるようになります。  
   たとえば、「CountTolerances」を「2」に設定すると、現在表示されているパスワードと1つ前のパスワードの両方でログインできます。デフォルトでは「1」に設定されており、その場合は最新のパスワードのみが有効です。

#### ②メールでの認証に切り替える

手元にTOTPに対応した端末がない場合に、[メールによる二段階認証](secondary-authentication.md)に切り替えることができます。

1. 確認コード入力欄の下の「メールで認証する」のリンクをクリックしてください。
1. 画面が[メールによる二段階認証](secondary-authentication.md)の確認コード入力欄に切り替わりますので、ユーザのメールアドレス宛に送付された確認コードを入力してください。

## アプリとの連携を解除する

認証アプリとの連携を解除するには、以下の手順を行います。

1. 「ユーザ管理機能」で解除したいユーザの詳細画面を開きます。
1. TOTP認証でログインしたユーザは「秘密鍵有効」にチェックが入っています。このチェックを外し、ユーザーを更新します。
   ![ユーザの詳細画面。「秘密鍵有効」のチェックを外して連携を解除する](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/c7dd3eafe1ff4da5b9250dde5f601ef9.png)
1. これで認証アプリに登録した情報は無効化され、確認コードではログインできなくなります。
1. プリザンターに再度ログインしようとすると、確認コード入力画面に再びQRコードが表示されます。ログインするには、このQRコードを使って認証アプリと再度連携してください。

## 関連情報

-   [パラメータ設定：Security.json](../../parameters/security-json.md)
-   [メールによる二段階認証を利用する](secondary-authentication.md)