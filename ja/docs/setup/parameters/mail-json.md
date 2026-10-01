---
title: Mail.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: mail-json
translationKey: mail-json
shortname: Mail.json
created: 2019-04-30
updated: 2026-07-14
---

## 注意事項

-   パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

=== "SMTPサーバを使用する場合"

    |パラメータ名|設定例|説明|
    |:--|:--|:--|
    |SmtpHost|"smtp.example.com"|SMTPサーバのアドレスを指定。|
    |SmtpPort|25|SMTPサーバのポートを指定。|
    |SmtpUserName|"UserName"|SMTP-AUTHのユーザ名を指定。<br>**システム環境変数に登録可能。**<br><br>null<br>ユーザ認証を行わない。|
    |SmtpPassword|"Password"|SMTP-AUTHのパスワードを指定。<br>**システム環境変数に登録可能。**<br><br>null<br>ユーザ認証を行わない。|

=== "SendGridを使用する場合"

    |パラメータ名|設定例|説明|
    |:--|:--|:--|
    |SmtpHost|"smtp.sendgrid.net"|SendGridのアドレスを指定。|
    |SmtpPort|0|SendGridを使用する場合には設定不要。|
    |SmtpUserName|"apikey"| ”apikey”（固定値）を指定。|
    |SmtpPassword|"SG.xxxxxxx"|SendGridのAPIキーを指定。|

    ``` json title="Mail.jsonをSendGrid用に構成する設定例"
    "SmtpHost": "smtp.sendgrid.net",
    "SmtpPort": 0,
    "SmtpUserName": "apikey",
    "SmtpPassword": "SG.xxxxAPIキーxxxxxx...",
    ```

!!! tip "OAuth 2.0認証を使いメールを送信するために必要な設定"
    「[プリザンターからM365のSMTPサーバを使ってメールを送信できるように設定する](../additional/notifications/smtp-oatuh.md)」を参照してください。

### 共通設定

|パラメータ名|設定例|説明|
|:--|:--|:--|
|SmtpEnableSsl|false|SSL/TLSを有効化する場合にはtrueを指定。trueに設定した場合、StartTlsの暗号化方式が適用されます。それ以外の方式を指定する場合はSecureSocketOptionsパラメータをご利用ください。|
|ServerCertificateValidationCallback|false|エラー「An error occurred while attempting to establish an SSL or TLS connection」の発生を抑制する場合はtrueを設定。|
|SecureSocketOptions|"SslOnConnect"|接続に使用する SSL/TLS 暗号化の方式を指定します。デフォルト値はnull。許容される文字列は MimeKitで利用可能な[Enumの名前](http://www.mimekit.net/docs/html/T_MailKit_Security_SecureSocketOptions.htm)を参照してください。|
|FixedFrom|"fixed@example.com"|メールアドレスを指定した場合、メール送信時のfromアドレスとなります。nullを設定した場合には、ログインユーザのメールアドレスがfromとなります。|
|AllowedFrom|[ "support@example.com" ]|FixedFromがnull以外の場合に、AllowedFromに列挙されたメールアドレスに該当する場合には、FixedFromが使用されずログインユーザのメールアドレスがfromとなります。|
|SupportFrom|"support@example.com"|サポート用メールアドレスを指定。[メールによる二段階認証](../additional/authn-authz/secondary-authentication.md)利用時は必須です。|
|InternalDomains|".example1.com,.example2.com"|メールの送信先ドメインを制限する場合には、ホワイトリストをカンマ区切りで指定。|
|AddressValidation|"\\b[A-Z0-9._%+-]+@[A-Z0-9.-]+\\.[A-Z]+\\b"|メールアドレスの検証に使用する正規表現を指定。|
|Encoding|"shift_jis"|デフォルト値は null 。UTF-8 以外に変更する場合に明示的に指定。なおシステムで利用できないエンコーディング名の場合、設定読み込み時に SysLogs にエラー出力したうえで UTF-8 で送信を試みます。|
|ContentEncoding|"SevenBit"| デフォルト値は null 。許容される文字列は MimeKit で利用可能な [Enum の名前](http://www.mimekit.net/docs/html/T_MimeKit_ContentEncoding.htm)を参照してください。|

## システム環境変数への登録方法

SmtpUserName、SmtpPassword、OAuthClientId、OAuthClientSecret、SendGrid.ApiKey、AwsSes.AccessKeyId、AwsSes.SecretAccessKey、AwsSes.SessionTokenは[システム環境変数に登録](credentials-in-environment-variables.md)できます。OAuthClientId、OAuthClientSecretは1.5.1.0以降、SendGrid.ApiKey、AwsSes.AccessKeyId、AwsSes.SecretAccessKey、AwsSes.SessionTokenは1.5.5.0以降で登録できます。

OAuthClientId、OAuthClientSecretは「[プリザンターからM365のSMTPサーバを使ってメールを送信できるように設定する](../additional/notifications/smtp-oatuh.md)」、SendGrid.ApiKeyは「[プリザンターからSendGridでメールを送信できるように設定する](../additional/notifications/sendgrid-mail.md)」、AwsSes.AccessKeyId、AwsSes.SecretAccessKey、AwsSes.SessionTokenは「[プリザンターからAWS SESでメールを送信できるように設定する](../additional/notifications/mail-aws-ses.md)」も参照してください。

!!! tip "システム環境変数への登録"
    システム環境変数への登録については以下のページも参照してください。  
    [パラメータ設定：資格情報をシステム環境変数に登録する](credentials-in-environment-variables.md)

### 1. 命名規則

システム環境変数の命名規則は以下の通りです。

``` text
（サービス名）_Mail_SmtpUserName
（サービス名）_Mail_SmtpPassword
（サービス名）_Mail_OAuthClientId
（サービス名）_Mail_OAuthClientSecret
（サービス名）_Mail_SendGrid_ApiKey
（サービス名）_Mail_AwsSes_AccessKeyId
（サービス名）_Mail_AwsSes_SecretAccessKey
（サービス名）_Mail_AwsSes_SessionToken
```

|項目|必須|説明|
|---|---|---|
|サービス名|○|[Service.json](service-json.md)の「EnvironmentName」または「Name」を指定|

#### 設定例

|変数|設定例|
|:--|:--|
|Implem.Pleasanter_Mail_SmtpUserName|UserName|
|Implem.Pleasanter_Mail_SmtpPassword|Password|
|Implem.Pleasanter_Mail_OAuthClientId|ClientId|
|Implem.Pleasanter_Mail_OAuthClientSecret|ClientSecret|
|Implem.Pleasanter_Mail_SendGrid_ApiKey|SG.xxxxAPIキーxxxxxx...|
|Implem.Pleasanter_Mail_AwsSes_AccessKeyId|AccessKeyId|
|Implem.Pleasanter_Mail_AwsSes_SecretAccessKey|SecretAccessKey|
|Implem.Pleasanter_Mail_AwsSes_SessionToken|SessionToken|

### 2. 優先順

本パラメータファイルとシステム環境の両方に設定した場合や省略形で設定した場合の優先順位は以下のとおりです。

=== "SmtpUserNameの優先順"

    |優先順|設定値|
    |:--|:--|
    |1|本パラメータファイルの「SmtpUserName」|
    |2|環境変数の「（サービス名：EnvironmentName）_Mail_SmtpUserName」|
    |3|環境変数の「（サービス名：Name）_Mail_SmtpUserName」|

=== "SmtpPasswordの優先順"

    |優先順|設定値|
    |:--|:--|
    |1|本パラメータファイルの「SmtpPassword」|
    |2|環境変数の「（サービス名：EnvironmentName）_Mail_SmtpPassword」|
    |3|環境変数の「（サービス名：Name）_Mail_SmtpPassword」|

=== "OAuthClientIdの優先順"

    |優先順|設定値|
    |:--|:--|
    |1|本パラメータファイルの「OAuthClientId」|
    |2|環境変数の「（サービス名：EnvironmentName）_Mail_OAuthClientId」|
    |3|環境変数の「（サービス名：Name）_Mail_OAuthClientId」|

=== "OAuthClientSecretの優先順"

    |優先順|設定値|
    |:--|:--|
    |1|本パラメータファイルの「OAuthClientSecret」|
    |2|環境変数の「（サービス名：EnvironmentName）_Mail_OAuthClientSecret」|
    |3|環境変数の「（サービス名：Name）_Mail_OAuthClientSecret」|

=== "SendGrid.ApiKeyの優先順"

    |優先順|設定値|
    |:--|:--|
    |1|本パラメータファイルの「SendGrid.ApiKey」|
    |2|環境変数の「（サービス名：EnvironmentName）_Mail_SendGrid_ApiKey」|
    |3|環境変数の「（サービス名：Name）_Mail_SendGrid_ApiKey」|
    |4|本パラメータファイルの「SmtpPassword」の値（SmtpHostが"smtp.sendgrid.net"で、Providerが"Smtp"の場合のみ。SmtpPasswordの値は「SmtpPasswordの優先順」のとおりに決まります）|

=== "AwsSes.AccessKeyIdの優先順"

    |優先順|設定値|
    |:--|:--|
    |1|本パラメータファイルの「AwsSes.AccessKeyId」|
    |2|環境変数の「（サービス名：EnvironmentName）_Mail_AwsSes_AccessKeyId」|
    |3|環境変数の「（サービス名：Name）_Mail_AwsSes_AccessKeyId」|

=== "AwsSes.SecretAccessKeyの優先順"

    |優先順|設定値|
    |:--|:--|
    |1|本パラメータファイルの「AwsSes.SecretAccessKey」|
    |2|環境変数の「（サービス名：EnvironmentName）_Mail_AwsSes_SecretAccessKey」|
    |3|環境変数の「（サービス名：Name）_Mail_AwsSes_SecretAccessKey」|

=== "AwsSes.SessionTokenの優先順"

    |優先順|設定値|
    |:--|:--|
    |1|本パラメータファイルの「AwsSes.SessionToken」|
    |2|環境変数の「（サービス名：EnvironmentName）_Mail_AwsSes_SessionToken」|
    |3|環境変数の「（サービス名：Name）_Mail_AwsSes_SessionToken」|

### 3. システム環境変数に登録する際の注意点

「2. 優先順」に記載の通りパラメータファイルに設定した値が最優先となるため、システム環境変数に登録する場合はパラメータファイルでは「null」を指定してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.18.0 以降|ServerCertificateValidationCallbackを追加|
|1.3.49.0 以降|SecureSocketOptionsを追加|
|1.5.1.0 以降|OAuthClientId、OAuthClientSecretをシステム環境変数に登録する機能を追加|
|1.5.5.0 以降|SendGrid.ApiKey、AwsSes.AccessKeyId、AwsSes.SecretAccessKey、AwsSes.SessionTokenをシステム環境変数に登録する機能を追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [プリザンターからM365のSMTPサーバを使ってメールを送信できるように設定する](../additional/notifications/smtp-oatuh.md)
-   [Enumの名前](http://www.mimekit.net/docs/html/T_MailKit_Security_SecureSocketOptions.htm)
-   [メールによる二段階認証を利用する](../additional/authn-authz/secondary-authentication.md)
-   [Enum の名前](http://www.mimekit.net/docs/html/T_MimeKit_ContentEncoding.htm)
-   [パラメータ設定：資格情報をシステム環境変数に登録する](credentials-in-environment-variables.md)
-   [パラメータ設定：Service.json](service-json.md)
