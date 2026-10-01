---
title: 資格情報をシステム環境変数に登録する
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: credentials-in-environment-variables
translationKey: credentials-in-environment-variables
shortname: 資格情報,システム環境変数,システム環境変数に登録
created: 2025-04-22
updated: 2026-08-12
---

## 概要

データベースへの接続文字列などの資格情報を記載したパラメータファイルがアクセス権設定不備などのミスから流出しても資格情報の漏洩を防ぐセキュリティの観点より、OSのシステム環境変数から資格情報を取得する機能がver.1.2.21.0より追加されました。資格情報をシステム環境変数に登録する手順について説明します。

## システム環境変数に登録できる資格情報

### [BinaryStorage.json](binary-storage-json.md)

Azure Blob Storageの接続文字列を設定できます。

|パラメータ|設定内容|
|---|---|
|AzureBlobStorageAccountUri|Azureストレージアカウントを含むURI形式の文字列です。（1.5.7.0以降）|
|AzureBlobContainerName|Azure Blobコンテナ名です。（1.5.7.0以降）|

### [Rds.json](rds-json.md)

データベースの接続文字列を設定できます。

|パラメータ|設定内容|
|---|---|
|SaConnectionString|データベースインスタンスにsa権限で接続するための接続文字列|
|OwnerConnectionString|Pleasanterのデータベースにdbowner権限で接続するための接続文字列を指定|
|UserConnectionString|Pleasanterのデータベースにdbreader,dbwriter権限で接続するための接続文字列を指定|
|MySqlConnectingHost|MySQLの場合のみ、MySQLへのユーザアクセス権について所定の方式で指定|

### [Mail.json](mail-json.md)

SMTP認証の情報と、メール送信サービスの認証情報を設定できます。

|パラメータ|設定内容|
|---|---|
|SmtpUserName|SMTP-AUTHのユーザ名を指定|
|SmtpPassword|SMTP-AUTHのパスワードを指定|
|OAuthClientId|OAuth 2.0認証でメールを送信する場合のクライアントIDを指定（1.5.1.0以降）|
|OAuthClientSecret|OAuth 2.0認証でメールを送信する場合のクライアントシークレットを指定（1.5.1.0以降）|
|SendGrid.ApiKey|SendGridのAPIキーを指定（1.5.5.0以降）|
|AwsSes.AccessKeyId|Amazon SESを使用する場合のAWSアクセスキーIDを指定（1.5.5.0以降）|
|AwsSes.SecretAccessKey|Amazon SESを使用する場合のAWSシークレットアクセスキーを指定（1.5.5.0以降）|
|AwsSes.SessionToken|Amazon SESを一時クレデンシャルで使用する場合のセッショントークンを指定（1.5.5.0以降）|

### [Security.json](security-json.md)

AspNetCoreDataProtectionの設定に関するパラメータをシステム環境変数に設定できます。

|パラメータ|設定内容|
|---|---|
|BlobContainerUri|データ保護キーを永続化するBlobコンテナのURLを指定|
|KeyIdentifier|データ保護キーを保護するための暗号化キーを管理するAzure Key Vaultのキー識別子を指定|
|XmlAesKey|データ保護キーを保護するための暗号化キーを生成するための文字列を指定|
|KeyValueStoreConnectionString|データ保護キーを保存するKVSの接続文字列を指定（1.5.7.0以降）|
|KeyValueStoreKeyName|KVSに保存するデータ保護キーの名前を指定（1.5.7.0以降）|

KeyValueStoreConnectionString、KeyValueStoreKeyNameについては「[ASP.NET Coreデータ保護キーを外部保存する](../additional/ready-for-clustering/data-protection-key-store.md)」を参照ください。

### [Service.json](service-json.md)

プリザンターのインストール環境を区別する文字列を設定できます。

|パラメータ|設定内容|
|---|---|
|DeploymentEnvironment|プリザンターがインストールされている環境（本番環境、ステージング環境など）を区別するための文字列を指定|

### [Kvs.json](kvs-json.md)

セッションデータの接続文字列を設定できます。

|パラメータ|設定内容|
|---|---|
|ConnectionStringForSession|セッションデータに接続するためのセッションの接続文字列を指定|

## システム環境変数の命名ルール

システム環境変数へ登録する際の変数名は以下の命名ルールに従ってください。詳細は各パラメータのマニュアルを参照ください。

```
 {サービス名}_{パラメータファイル名}_{パラメータ名}
```

1.  サービス名  
[Service.json](service-json.md)の「EnvironmentName」または「Name」を指定します。優先順は「EnvironmentName」→「Name」です。
2. パラメータファイル名  
パラメータファイル名を指定します。データベース接続文字列をシステム環境変数に登録する場合は「Rds」と指定します。
3. パラメータ名  
システム環境変数に登録したいパラメータ名を指定します。SendGrid.ApiKeyのように階層を持つパラメータは、「.」を「_」に置き換えます（例：（サービス名）_Mail_SendGrid_ApiKey）。

※データベース接続文字列はデータベース種類もシステム環境変数名に指定できます。詳細は[Rds.json](rds-json.md)を参照ください。

## パラメータの優先順

パラメータファイルとシステム環境の両方に設定した場合の優先順は以下のとおりです。詳細は各パラメータのマニュアルを参照ください。

|優先順|設定値|
|---|---|
|1|パラメータファイルの設定値|
|2|システム環境変数の「{サービス名（EnvironmentName）}\_{パラメータファイル名}\_{パラメータ名}」|
|3|システム環境変数の「{サービス名（Name）}\_{パラメータファイル名}\_{パラメータ名}」|

※データベース接続文字列はデータベース種類も加味した優先順となります。詳細は[Rds.json](rds-json.md)を参照ください。

## システム環境変数に登録する場合の注意点

資格情報をシステム環境変数に登録する場合は、パラメータファイルでは「null」を設定してください。上述の優先順の通り、パラメータファイル、システム環境変数両方に設定するとパラメータファイルの内容が優先されます。

## システム環境変数の登録方法

### 1. App Service

1. Azure Portalに接続し、作成済みのApp Serviceインスタンスを選択します。
1. 左側のメニューの「設定」－「環境変数」をクリックします。
1. 「アプリ設定」タブの「＋追加」ボタンをクリックします。
1. 登録するしたい資格情報の「名前」と「値」を入力し、「適用」ボタンをクリックします。

### 2. Windows

1. スタートメニューから「システム環境変数の編集」を検索し、起動します。
1. 「システムのプロパティ」ダイアログ「詳細設定」タブの「環境変数」ボタンをクリックします。
1. 「環境変数」ダイアログの「システム環境変数」の「新規」ボタンをクリックします。
1. 「新しいシステム変数」ダイアログにて登録するしたい資格情報の「変数名」と「変数値」を入力し、「OK」ボタンをクリックします。
1. 「環境変数」ダイアログの「OK」ボタンをクリックし、「システムのプロパティ」ダイアログの「OK」ボタンをクリックします。

### 3. Linux

**Linuxの/etc/profileにシステム環境変数を設定する場合、システム環境変数名に「.（ドット）」が含まれる場合にエラーになる場合があります。その際は以下のいずれかの手順でシステム環境変数を設定してください。**
1. envコマンドを利用して登録
2. Pleasanterサービス用スクリプト（/etc/systemd/system/pleasanter.service）に追記する。  
    ここではデータベース接続文字列を指定する例を記載します。
    - 追記前
```
～
[Service]
ExecStart = /usr/local/bin/dotnet Implem.Pleasanter.dll
～
```

    - 追記後
```
～
[Service]
ExecStart=/usr/bin/env \
Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString="Server=localhost;Port=5432;Database=postgres;UID=postgres;PWD=SetSaPWD" \
Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString="Server=localhost;Port=5432;Database=Implem.Pleasanter;UID=Implem.Pleasanter_Owner;PWD=SetAdminsPWD" \
Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString="Server=localhost;Port=5432;Database=Implem.Pleasanter;UID=Implem.Pleasanter_User;PWD=SetUsersPWD" \
/usr/local/bin/dotnet Implem.Pleasanter.dll
～
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.21.0 以降|資格情報をシステム環境変数に登録できる機能を追加|
|1.3.26.0 以降|Service.jsonのDeploymentEnvironmentを対象に追加|
|1.4.16.0 以降|Kvs.jsonのConnectionStringForSessionを対象に追加|
|1.4.18.0 以降|Rds.jsonのMySqlConnectingHostを対象に追加|
|1.5.1.0 以降|Mail.jsonのOAuthClientId、OAuthClientSecretを対象に追加|
|1.5.5.0 以降|Mail.jsonのSendGrid.ApiKey、AwsSes.AccessKeyId、AwsSes.SecretAccessKey、AwsSes.SessionTokenを対象に追加|
|1.5.7.0 以降|BinaryStorage.jsonのAzureBlobStorageAccountUri、AzureBlobContainerName、Security.jsonのKeyValueStoreConnectionString、KeyValueStoreKeyNameを対象に追加|

## 関連情報

-   [BinaryStorage.json](binary-storage-json.md)
-   [Rds.json](rds-json.md)
-   [Mail.json](mail-json.md)
-   [Security.json](security-json.md)
-   [Service.json](service-json.md)
-   [Kvs.json](kvs-json.md)

