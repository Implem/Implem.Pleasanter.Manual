---
title: Microsoft Entra IDによるシングルサインオンを利用する
category: 追加設定：認証
order: '0'
status: ''
parts: ''
urlstring: ms-entra-id-sso
translationKey: ms-entra-id-sso
shortname: ''
created: 2026-06-15
updated: 2026-06-23
---

## 概要

Microsoft Entra IDによるシングルサインオンを利用するための設定手順です。

## 制限事項

1. Pleasanter.net共有環境ではSAML認証は利用できません。
1. プリザンターにはSPメタデータを発行する機能がありません。SP側のメタデータをIdPに登録することはできません。
1. 運用環境ではhttpsを使用してください。httpはローカル検証・開発用途に限ります。

## 前提条件

1. Microsoft Entra IDのテナントが存在し、エンタープライズアプリケーションを作成する権限があること。

## 操作手順

### 1. Entra ID側にエンタープライズアプリケーションを作成する

1. [Microsoft Entra 管理センター](https://entra.microsoft.com) にサインインしてください。
1. 画面左のメニューから「エンタープライズ アプリ」を開き、「新しいアプリケーション」をクリックしてください。
1. 「独自のアプリケーションの作成」を選択し、アプリ名（例：Pleasanter）を入力して「作成」してください。
1. 作成したアプリケーションを開き、「シングル サインオン」→[SAML](saml.md)を選択してください。

### 2. Entra ID側にSP情報を登録する

1. 「基本的なSAML構成」セクションの「編集」をクリックし、以下の値を入力してください。  
       【サーバ名】はプリザンターが動作しているサーバのURLに置き換えてください。

       | 項目 | 設定値 |
       |---|---|
       | 識別子 (Entity ID) | 【サーバ名】/Saml2 |
       | 応答 URL (ACS URL) | 【サーバ名】/Saml2/Acs |

1. 入力後、「保存」をクリックしてください。

### 3. メタデータURLとテナント情報を取得する

以下の手順で[Authentication.json](../../parameters/authentication-json.md)の設定に必要な値を取得してください。

1. 同じシングル サインオン設定画面で、「SAML 署名証明書」セクションにある「アプリのフェデレーション メタデータ URL」を控えてください。これがMetadataLocationに設定する値です。
1. 「属性とクレーム」セクションを開き、「Microsoft Entra 識別子」の値（https://sts.windows.net/【テナントID】/ の形式）を控えてください。これがEntityIdに設定する値です。
1. アプリケーションの「プロパティ」から「アプリケーション ID」を控えてください。これがMetadataLocationのURLに含まれるappidパラメータの値です。

### 4. Authentication.jsonを編集する

プリザンターサーバ上の[Authentication.json](../../parameters/authentication-json.md)を開き、以下の設定例を参考に編集してください。

1. SPOptions.EntityIdとSPOptions.ReturnUrlの【サーバ名】は、手順2でEntra IDに登録した「識別子 (Entity ID)」および「応答 URL」と一致させてください。
1. 【テナントID】と【アプリID】は、手順3で取得した値に置き換えてください。

    ```json
    {
        "Provider": "SAML",
        "SamlParameters": {
            "Attributes": {
                "Name": "Name",
                "UserCode": "UserCode",
                "Birthday": "Birthday",
                "Gender": "Gender",
                "Language": "Language",
                "TimeZone": "TimeZone",
                "TenantManager": "TenantManager",
                "DeptCode": "DeptCode",
                "Dept": "Dept",
                "Body": "Body",
                "MailAddress": "{NameId}"
            },
            "SamlTenantId": 1,
            "DisableOverwriteName": false,
            "NotCreatePersistentCookie": false,
            "SPOptions": {
                "EntityId": "https://【サーバ名】/Saml2",
                "ReturnUrl": "https://【サーバ名】/Users/SamlLogin",
                "AuthenticateRequestSigningBehavior": "IfIdpWantAuthnRequestsSigned",
                "OutboundSigningAlgorithm": "https://www.w3.org/2001/04/xmldsig-more#rsa-sha256",
                "MinIncomingSigningAlgorithm": "https://www.w3.org/2001/04/xmldsig-more#rsa-sha256",
                "IgnoreMissingInResponseTo": false,
                "PublicOrigin": null,
                "ServiceCertificates": []
            },
            "IdentityProviders": [
                {
                    "EntityId": "https://sts.windows.net/【テナントID】/",
                    "SignOnUrl": "https://login.microsoftonline.com/【テナントID】/saml2",
                    "LogoutUrl": null,
                    "AllowUnsolicitedAuthnResponse": true,
                    "Binding": "HttpPost",
                    "WantAuthnRequestsSigned": false,
                    "DisableOutboundLogoutRequests": true,
                    "LoadMetadata": true,
                    "MetadataLocation": "https://login.microsoftonline.com/【テナントID】/FederationMetadata/2007-06/FederationMetadata.xml?appid=【アプリID】",
                    "SigningCertificate": null
                }
            ]
        }
    }
    ```

### 5. IISを再起動して動作確認する

1. IISを再起動してください。
1. ブラウザでプリザンターにアクセスしてください。
1. ログイン画面に「SSOログイン」ボタンが表示されていることを確認し、クリックしてEntra IDでのログインを確認してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.8.0 以降|NotCreatePersistentCookieを追加|
|1.2.6.0 以降|機能追加|

## 関連情報

-   [Microsoft Entra 管理センター](https://entra.microsoft.com)
-   [SAML認証を利用する](saml.md)