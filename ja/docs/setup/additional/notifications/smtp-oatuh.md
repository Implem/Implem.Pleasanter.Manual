---
title: プリザンターからM365のSMTPサーバを使ってメールを送信できるように設定する
category: 追加設定：通知
order: '0'
status: ''
parts: ''
urlstring: smtp-oatuh
translationKey: smtp-oatuh
shortname: ''
created: 2026-01-23
updated: 2026-06-09
---

## 概要

プリザンターからMicrosoft 365のSMTPサーバでOAuth 2.0認証を使い、メールを送信するために必要な設定について説明します。マイクロソフト社はSMTPサーバの認証方式を[ベーシック認証からOAuth 2.0認証へ移行](https://jpmessaging.github.io/blog/Updated-Exchange-Online-SMTP-AUTH-Basic-Authentication-Deprecation-Timeline/)させており、この変更に伴う対応が必要な場合は、以下の情報を確認してください。

本マニュアルでは、Microsoft 365側の設定と、プリザンター側の設定とに分けて説明します。Microsoft 365側の設定については概略を示すにとどめます。詳細は本マニュアルの末尾にまとめたマイクロソフト社のドキュメントを確認してください。

## 前提条件

1. Microsoft 365 テナントの管理者権限が必要です。
1. Entra ID（旧Azure Active Directory）へのアクセス権限が必要です。
1. 事前に送信に使用するメールボックス（共有メールボックスまたはユーザメールボックス）の作成が必要です。
1. 管理者権限で実行できるWindows PowerShellが必要です。

## 1. Microsoft 365側の設定

### 1.1. アプリケーションの登録

管理者権限を持つアカウントで[Microsoft Azure Portal](https://portal.azure.com) にサインインし、アプリケーションを新規登録してください。登録後、以下の情報をメモしてください。

| 項目 | 説明 |
|------|------|
| アプリケーション (クライアント) ID| パラメータOAuthClientIdに設定します。 |
| ディレクトリ (テナント) ID|パラメータOAuthTokenEndpointに設定する値の一部として使用します。 |

### 1.2. クライアントシークレットの作成

「新しいクライアント シークレット」を作成・追加してください。表示された「値」をコピーして安全な場所に保存してください。<span class="pl-attention">シークレットの値は一度しか表示されません。必ずコピーして保存してください。</span>保存した値は、後ほどパラメータOAuthClientSecretに設定します。

| 項目 | 説明 |
|------|------|
|値| <span class="pl-attention">作成時に一度しか表示されません。</span>パラメータOAuthClientSecretに設定します。|

### 1.3. APIアクセス許可の設定

Office 365 Exchange Onlineに対し、SMTP.SendAsAppの許可を追加してください。
また、当該テナントへ管理者の同意を付与してください。<span class="pl-attention">この操作は、テナントの全体管理者の権限が必要です。</span>

### 1.4. テナント全体のSMTP AUTH設定

PowerShellを使い、テナント全体に対してSMTP AUTHを有効化してください。

この操作には、Exchange OnlineのOrganization Management（組織管理）ロールグループに属する権限が必要です。

### 1.5. Exchange Onlineの設定

PowerShellを使い、以下を実施してください。

1. **送信用共有メールボックスの作成**  
   [Exchangeの管理ポータル](https://admin.cloud.microsoft/#/homepage)にアクセスし、送信用の共有メールボックスを作成してください。

2. **サービスプリンシパルの登録**  
   Exchange Online PowerShellに接続して、アプリケーションにSMTP送信権限を付与してください。  
   この操作には、Organization Management（組織管理）ロールグループに属する権限が必要です。

3. **メールボックスへのアクセス許可を付与**  
   送信に使用するメールボックスに対してアクセス許可を付与してください。  
   この操作には、Organization Management（組織管理）またはRecipient Management（受信者管理）ロールグループに属する権限が必要です。

## 2. プリザンター側の設定

### 2.1. Mail.jsonの設定

設定ファイル[Mail.json](../../parameters/mail-json.md)のパラメータを以下のように設定してください。

```json
{
    "SmtpHost": "smtp.office365.com",
    "SmtpPort": 587,
    "SmtpUserName": "{{送信用共有メールボックスの所有者のメールアドレス}}",
    "SmtpPassword": "",
    "SmtpEnableSsl": true,
    "SecureSocketOptions": "StartTls",
    "UseOAuth": true,
    "OAuthClientId": "{{アプリケーション (クライアント) ID}}",
    "OAuthClientSecret": "{{クライアントシークレットの値}}",
    "OAuthScope": "https://outlook.office365.com/.default",
    "OAuthGrantType": "client_credentials",
    "OAuthTokenEndpoint": "https://login.microsoftonline.com/{{ディレクトリ (テナント) ID}}/oauth2/v2.0/token",
    "Encoding": "UTF-8",
    "FixedFrom": "{{送信用共有メールボックスの所有者のメールアドレス}}",
    "SupportFrom": "{{送信用共有メールボックスの所有者のメールアドレス}}"
}
```

#### 設定項目の説明

【固定値】とある設定項目には、既定の値を設定してください。

| パラメータ | 値 | 説明 |
|-----------|-----|------|
| SmtpHost | smtp.office365.com | M365のSMTPサーバ【固定値】|
| SmtpPort | 587 | SMTP送信ポート【固定値】 |
| SmtpUserName | {{送信用共有メールボックスの所有者のメールアドレス}}| SMTP-AUTHのユーザ名を指定。 |
| SmtpPassword | 空欄 | OAuth使用時は不要【固定値】 |
| SmtpEnableSsl | true | SSL/TLS有効化【固定値】 |
| SecureSocketOptions | StartTls | STARTTLS使用【固定値】 |
| UseOAuth | true | OAuth認証を有効化【固定値】 |
| OAuthClientId | {{アプリケーション (クライアント) ID}}（空欄""を推奨） | Azure Portalで取得したクライアントID<br><span class="pl-attention">※下記参照</span> |
| OAuthClientSecret | {{クライアントシークレットの値}}（空欄""を推奨）| Azure Portalで作成したクライアントシークレットの「値」<br><span class="pl-attention">※下記参照</span> |
| OAuthScope | https://outlook.office365.com/.default | M365 SMTPのスコープ【固定値】 |
| OAuthGrantType | client_credentials | クライアント資格情報フロー【固定値】 |
| OAuthTokenEndpoint | https://login.microsoftonline.com/{{ディレクトリ (テナント) ID}}/oauth2/v2.0/token | トークンエンドポイント（{{ディレクトリ (テナント) ID}}をAzure Portalで取得した実際の値に置換） |
| Encoding | UTF-8 | メール本文のエンコーディング形式【固定値】 |
| FixedFrom | {{送信用共有メールボックスの所有者のメールアドレス}} | メール送信時のfromアドレス。OAuth 2.0認証時には送信用共有メールボックスの所有者のメールアドレスを設定 |
| SupportFrom | {{送信用共有メールボックスの所有者のメールアドレス}} | サポート用メールアドレスを指定。OAuth 2.0認証時には送信用共有メールボックスの所有者のメールアドレスを設定 |

### 2.2. OAuthClientIdとOAuthClientSecretを環境変数で設定する

セキュリティ上の理由から、以下のパラメータは環境変数で設定することを推奨します。

1. OAuthClientId
1. OAuthClientSecret

#### Linux/macOS Bash

```sh
export Pleasanter_Mail_OAuthClientId="{{アプリケーション (クライアント) ID}}"
export Pleasanter_Mail_OAuthClientSecret="{{クライアントシークレットの値}}"
```

#### Windows PowerShell

```ps1
$env:Pleasanter_Mail_OAuthClientId = "{{アプリケーション (クライアント) ID}}"
$env:Pleasanter_Mail_OAuthClientSecret = "{{クライアントシークレットの値}}"
```

1. 環境変数名のプレフィックスは{EnvironmentName}_Mail_または{ServiceName}_Mail_の形式です。
1. デフォルトのServiceNameはPleasanterです。
1. 環境変数で設定する場合、[Mail.json](../../parameters/mail-json.md)のOAuthClientIdとOAuthClientSecretは空欄（""）にしてください。

すべての設定が済んだら、プリザンターを再起動してください。

## 3. エラーが表示された場合の確認事項

##### エラー: "OAuth token acquisition failed"が表示される

1. OAuthClientId、OAuthClientSecret、OAuthTokenEndpointの値を確認してください。
1. EntraアプリケーションのAPI許可が正しく付与されているかを確認してください。
1. 管理者の同意が付与されているかを確認してください。

##### エラー: "Authentication failed"が表示される

1. SmtpUserNameが正しいメールアドレスかを確認してください。
1. Exchange Onlineでサービスプリンシパルが正しく登録されているかを確認してください。
1. メールボックスへのアクセス許可が付与されているかを確認してください。

##### エラー: "5.7.3 Authentication unsuccessful"が表示される

1. OAuthScopeがhttps://outlook.office365.com/.default になっているかを確認してください。
1. SMTP AUTH がメールボックスで有効になっているかを確認してください。

## 4. セキュリティに関する注意事項

|セキュリティ項目|推奨事項|
|:--|:--|
|クライアントシークレットの管理|シークレットは定期的にローテーションしてください。<br>有効期限が切れる前に新しいシークレットを作成し、設定を更新してください。|
|最小権限の原則の遵守|必要最小限のAPI許可のみを付与してください。<br>特定のメールボックスのみにアクセス許可を限定してください。|
|監査ログの確認|Entra IDのサインインログを定期的に確認してください。<br>不審なアクティビティがないかを監視してください。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.1.0 以降|機能追加|

## 関連情報

- [Microsoft: Authenticate an IMAP, POP or SMTP connection using OAuth](https://learn.microsoft.com/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth)
- [Microsoft: Register an application with the Microsoft identity platform](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)
- [Microsoft: SMTP AUTH clients submission](https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission)
