---
title: SAML認証を利用する
category: 追加設定：認証
order: '600'
status: ''
parts: ''
urlstring: saml
translationKey: saml
shortname: SAML,SAML認証
created: 2021-09-09
updated: 2026-08-12
---

## 制限事項

1. Pleasanter.net共有環境ではSAML認証は利用できません。
1. PleasanterにSP（Pleasanter）側のメタデータを発行する機能はありません。SP（Pleasanter）のメタデータをIdPに登録して連携することはできません。
1. 運用時のプロトコルとしてはhttpsを推奨します。httpはローカル検証用途・開発用途などに限って使用してください。
1. Linux環境では、SigningCertificateで指定する証明書のストア配置手順が、ディストリビューションやOSバージョンにより異なる場合があります。証明書配置に困難が生じる場合は、**IdPがメタデータURLを提供している場合に限り**、LoadMetadata: trueとMetadataLocationを使用した方式を代替として利用できます（詳細は[「MetadataLocationを利用したメタデータ自動取得」](#autogetmd)を参照してください）。

## 概要

SAML認証を利用するための設定手順を記載します。

## 1. Authentication.jsonをSAML認証向けに構成

[Authentication.json](../../parameters/authentication-json.md)を編集し、SAML認証向けに構成します。  

##### Authentication.json設定例（SAML認証に関連する項目のみを抜粋）

```json
{
    "Provider": "SAML",
    // ～中略～
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
            "EntityId": "https://localhost:59802/Saml2",
            "ReturnUrl": "https://localhost:59802/Users/SamlLogin",
            "AuthenticateRequestSigningBehavior": "IfIdpWantAuthnRequestsSigned",
            "OutboundSigningAlgorithm": "https://www.w3.org/2001/04/xmldsig-more#rsa-sha256",
            "MinIncomingSigningAlgorithm": "https://www.w3.org/2001/04/xmldsig-more#rsa-sha256",
            "IgnoreMissingInResponseTo": false,
            "PublicOrigin": null,
            "ServiceCertificates": []
        },
        "IdentityProviders": [
            {
                "EntityId": null,
                "SignOnUrl": null,
                "LogoutUrl": null,
                "AllowUnsolicitedAuthnResponse": true,
                "Binding": "HttpPost",
                "WantAuthnRequestsSigned": false,
                "DisableOutboundLogoutRequests": true,
                "LoadMetadata": false,
                "MetadataLocation": null,
                "SigningCertificate": {
                    "StoreName": "My",
                    "StoreLocation": "CurrentUser",
                    "X509FindType": "FindByThumbprint",
                    "FindValue": null
                }
            }
        ]
    }
}
```

## Authentication.jsonのSAML認証項目

|項目名|設定例|説明|
|-|-|-|
|Provider|SAML|SAMLを指定します。|
|SamlParameters.Attributes|JSONオブジェクト|下記<a href="#Attributes">SamlParameters.Attributes項目一覧</a>を参照。|
|SamlParameters.SamlTenantId|1|1固定|
|SamlParameters.DisableOverwriteName|false|ログイン時にユーザの「名前」をSAMLレスポンスの値で上書きしたくない場合にtrueを設定します。|
|SamlParameters.NotCreatePersistentCookie|false|SAML認証時に認証クッキーを永続化できないようにします。|
|SamlParameters.SPOptions|JSONオブジェクト|下記<a href="#SPOptions">SamlParameters.SPOptions項目一覧</a>を参照。|
|SamlParameters.IdentityProviders|JSONオブジェクト|下記<a href="#IdentityProviders">SamlParameters.IdentityProviders項目一覧</a>を参照|

<a id="Attributes"></a>

### SamlParameters.Attributes項目一覧

プリザンターのユーザ項目とSAMLレスポンスから取得可能な属性名との対応付けを行います。パラメータの左側（キー）がプリザンターのユーザ項目です。対応するSAMLレスポンスの属性名を右側に記載します。

|ユーザ項目名|既定値|説明|
|-|-|-|
|Name|Name|「名前」に設定する属性名を指定。FirstName,LastNameの項目を追加している場合、Nameにnullを指定することで、FirstNameとLastNameを組み合わせた値をNameに設定します。指定したSAML属性から値が取得できなかった場合、ログインIDが設定されます。詳細は「[FAQ：SAML認証で、ユーザー項目を「Name」の代わりに「givenName」と「surname」を結合して指定したい](../../../FAQ/system-requirements-and-setup/faq-saml-sync-user-item-name.md)」を参照してください。|
|UserCode|UserCode|「ユーザコード」に設定する属性名を指定します。|
|Birthday|Birthday|「生年月日」に設定する属性名を指定します。|
|Gender|Gender|「性別」に設定する属性名を指定します。|
|Language|Language|「 言語 」に設定する属性名を指定します。|
|TimeZone|TimeZone|「 タイムゾーン 」に設定する属性名を指定します。|
|TenantManager|TenantManager|「 テナント管理者 」に設定する属性名を指定します。属性値がtrueの場合にそのユーザがテナント管理者として登録されます。|
|DeptCode|DeptCode|「組織コード」に設定する属性名を指定します。ここで取得した組織コードを持つ「 組織 」がこのユーザに割り当てられます。該当する「 組織 」が存在しなかった場合は新しい組織が作成されます。詳細は「[FAQ：SAML認証で、ユーザ項目の「DeptCode」を指定せずに組織に反映したい](../../../FAQ/system-requirements-and-setup/faq-saml-sync-user-item-dept.md)」を参照してください。|
|Dept|Dept|「組織名」に設定する属性名を指定します。「DeptCode」から引き当てた「 組織 」の組織名を更新します。該当する組織が存在しなかった場合はこの「組織名」で組織が作成されます。|
|Body|Body|「 説明 」に設定する属性名を指定します。|
|MailAddress|{NameId}|「メールアドレス」に設定する属性名を指定します。NameID要素がメールアドレスの場合、{NameId}と指定することでNameIDの値を「メールアドレス」として登録可能です。|

#### ユーザ項目の同期について

SAML認証でのログインが成功すると、SAMLレスポンスから渡されるユーザデータを基に、プリザンターのユーザを作成・更新します。

1. SAMLレスポンスのNameID要素に設定されているIDを「ログインID」として登録します。
1. 未登録の「ログインID」であった場合、その「ログインID」でユーザが新規に作成されます。
1. 登録済みの「ログインID」であった場合、その「ログインID」のユーザ情報が更新されます。
1. 同期するユーザ情報は[Authentication.json](../../parameters/authentication-json.md)の__SamlParameters.Attributes__ で指定したSAMLレスポンスの属性名で検索します。SAMLレスポンスの該当する属性名が存在したのみ、その値をユーザ項目に設定します。

ユーザ項目と同期するSAMLレスポンスの属性名が不明の場合、SAMLログイン時に受け取ったレスポンスデータから確認する方法があります。確認手順は下記のリンク先を確認してください。  
[SAML認証設定でAuthentication.json に設定するSAMLレスポンスの属性名を確認したい](../../../FAQ/system-requirements-and-setup/faq-saml-response.md)

<a id="SPOptions"></a>

### SamlParameters.SPOptions項目一覧

このセクションでは、サービスプロバイダ（＝プリザンター）側の情報を設定します。  
説明列の文字列【サーバ名】は環境に応じて読み替えてください。

|要素名|設定例|説明|
|-|-|-|
|EntityId|https://sso-pleasanter.com/pleasanter/Saml2|サービスプロバイダのEntity ID。<br>【サーバ名】/Saml2を指定します。|
|ReturnUrl|https://sso-pleasanter.com/pleasanter/Users/SamlLogin|認証成功後に遷移するリダイレクト先。<br>【サーバ名】/Users/SamlLoginを指定します。|
|AuthenticateRequestSigningBehavior|IfIdpWantAuthnRequestsSigned||
|OutboundSigningAlgorithm|https://www.w3.org/2001/04/xmldsig-more#rsa-sha256||
|MinIncomingSigningAlgorithm|https://www.w3.org/2001/04/xmldsig-more#rsa-sha256||
|IgnoreMissingInResponseTo|false|SAMLレスポンスに含まれるInResponseTo要素の検証をスキップする場合にtrueを設定します。|
|PublicOrigin|null|Saml2エンドポイントのベースURLを指定します。リバースプロキシやロードバランサーを使用している場合など、サーバ内のURLと外部に公開しているURLが異なる場合に使用します。|
|ServiceCertificates|[]||

<a id="IdentityProviders"></a>

### SamlParameters.IdentityProviders項目一覧

このセクションでは、IDプロバイダ側の情報を設定します。

|要素名|設定例|説明|
|-|-|-|
|EntityId|https://id-provider.com/saml|IDプロバイダのEntity IDを指定します。|
|SignOnUrl|https://id-provider.com/saml/login|IDプロバイダのログインURLを指定します。|
|LogoutUrl|null||
|AllowUnsolicitedAuthnResponse|true|非要請応答を許可します。IdP-Initiatedを利用する場合はtrueを指定します。|
|Binding|HttpPost|SAMLリクエストをIDプロバイダに送信する際に使用するバインディング。以下の値が設定可能です。<br>・HttpRedirect<br>・HttpPost<br>・Artifact|
|WantAuthnRequestsSigned|false||
|DisableOutboundLogoutRequests|true||
|LoadMetadata|false|true<br>MetadataLocationに設定したURLまたはファイルパスからメタデータを取得し、IdPの構成（署名証明書・エンドポイント等）を自動的に読み込みます。<br><br>false（既定値）<br>MetadataLocationは無視されます。|
|MetadataLocation|null|LoadMetadataがtrueの場合に参照するIdPのメタデータのURLまたはファイルパスを指定します。URL（例: Entra IDのフェデレーションメタデータURL）またはサーバ上のXMLファイルの絶対パスを指定できます。<br>LoadMetadataがfalseの場合は無視されます。|
|SigningCertificate|<a href="#SigningCertificate">（下記参照）</a>|IdPがメッセージの署名に使用する証明書の情報を設定します。LoadMetadata: trueを使用する場合、メタデータから証明書が自動取得されるためnullを指定できます。nullの場合は証明書ストアへのアクセスは行われません。<br>以下の<a href="#SigningCertificate">SamlParameters.IdentityProviders.SigningCertificate項目一覧</a>も参照してください。|

<a id="autogetmd"></a>

### MetadataLocationを利用したメタデータ自動取得

LoadMetadata: trueとMetadataLocationを組み合わせることで、IdPが提供するメタデータから署名証明書・エンドポイント情報を自動取得できます。この方式では、SigningCertificateにnullを指定するため、IdPの証明書をサーバにインストールする作業が不要になります。

#### この方式が有効なケース

1. Linux環境で.NETの証明書ストアへの証明書配置が困難な場合
1. IdPがフェデレーションメタデータURLを提供している場合（Microsoft Entra IDなど）
1. 証明書の期限切れ時に自動更新されるメタデータを利用したい場合

#### MetadataLocation設定時の注意事項

1. MetadataLocationにはインターネットまたはサーバローカルからアクセス可能なURLまたはファイルパスを指定してください。
1. プリザンターからMetadataLocationのURLへのアクセスが遮断されている場合（ファイアウォールなど）はメタデータの取得に失敗します。その場合はメタデータXMLファイルをサーバにダウンロードし、ファイルパスで指定してください。
1. ユーザ環境において事前検証を実施したうえで判断・利用してください。弊社での動作確認実績については、以下の[設定例](#mseid)を参照してください。

<a id="SigningCertificate"></a>

#### SamlParameters.IdentityProviders.SigningCertificate項目一覧

このセクションでは、IDプロバイダがメッセージの署名に使用する証明書の情報を設定します。

|要素名|設定例|説明|
|-|-|-|
|StoreName|My|検索する証明書ストア名。設定可能な値は[マイクロソフト社のドキュメント](https://docs.microsoft.com/ja-jp/dotnet/api/system.security.cryptography.x509certificates.storename)を参照。|
|StoreLocation|LocalMachine|検索する証明書ストア。設定可能な値は[マイクロソフト社のドキュメント](https://docs.microsoft.com/ja-jp/dotnet/api/system.security.cryptography.x509certificates.storelocation)を参照。|
|X509FindType|FindByThumbprint|findValueの値との一致を検索するフィールド。設定可能な値は[マイクロソフト社のドキュメント](https://docs.microsoft.com/ja-jp/dotnet/api/system.security.cryptography.x509certificates.x509findtype)を参照。|
|FindValue|50B459426DE554010B35E9XXXXXXXXXXXXXXXXX|証明書を検索する際の検索値。x509FindTypeで指定したフィールドで検索を行います。以下を参照。|

##### FindValueに設定する証明書の検索値（拇印）の確認方法

以下の手順で確認できます。より詳細な情報は、[Sustainsys.Saml2のドキュメント](https://saml2.sustainsys.com/en/v2/configuration.html#sustainsys-saml2-section)を参照してください。

1. Windowsキーを押しながら、Rキーを押してください。
1. 「ファイル名を指定して実行」ダイアログに「certlm.msc」と入力し、「OK」ボタンをクリックしてください。
2. 「管理コンソール」の「個人」－「証明書」から対象の証明書をダブルクリックしてください。
3. 「証明書情報」画面の「詳細」タブ－「拇印」フィールドの「値」に表示される文字列を確認してください。

<a id="mseid"></a>

### 設定例: Microsoft Entra ID（MetadataLocation方式）

Microsoft Entra IDをIdPとする場合、以下のようにLoadMetadata: trueとMetadataLocationを使用する構成を利用できます。

#### Entra ID管理ポータルでの確認手順（メタデータURLの取得）

1. [Microsoft Entra 管理センター](https://entra.microsoft.com) にサインインしてください。
2. **エンタープライズ アプリケーション** > 対象アプリ > **シングル サインオン**を開いてください。
3. **SAML 署名証明書**セクションにある**「アプリのフェデレーション メタデータ URL」** をコピーしてください。

#### Authentication.json設定例（IdentityProviders部分の抜粋）

以下の設定例において、<span style="background:black;color:#96d0ff">【テナントID】</span>と<span style="background:black;color:#96d0ff">【アプリID】</span>の部分は、Entra IDテナントの実際の値に置き換えてください。

##### JSON

```json
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
```

| 項目 | 取得元 |
|---|---|
| <span style="background:black;color:#96d0ff">【テナントID】</span> | Entra ID 管理センター > エンタープライズ アプリ > シングル サインオン設定画面の **「Microsoft Entra 識別子」** |
| <span style="background:black;color:#96d0ff">【アプリID】</span> | Entra ID 管理センター > エンタープライズ アプリ > アプリケーション プロパティの **「アプリケーション ID」** |
| MetadataLocation全体 | 管理センターの **「アプリのフェデレーション メタデータ URL」** をそのまま貼り付け |

**補足**: EntityIdおよびSignOnUrlはMetadataLocation取得時に上書きされる場合があります。Entra IDの場合、メタデータに含まれる値と一致していれば問題ありません。

**注意**: SPOptionsのEntityId（例: https://[サーバ名]/Saml2）およびReturnUrlは、Entra IDのエンタープライズアプリケーション登録時に設定した **識別子 (Entity ID)**および**応答 URL (ACS URL)**と一致させる必要があります。

## 2. IDプロバイダ側の設定

IDプロバイダ側の設定は、各IDプロバイダのドキュメントに従い、設定してください。  
IDプロバイダ側で必要と思われるプリザンター側の情報は以下の通りです。  
値列の【サーバ名】は環境に応じて読み替えてください。

|項目名|値<br>設定例|
|:--|:--|
|SPのEntity ID|【サーバ名】/Saml2<br>https://sso-pleasanter.com/pleasanter/Saml2|
|認証成功後に遷移するリダイレクトURL|【サーバ名】/Users/SamlLogin<br>https://sso-pleasanter.com/pleasanter/SamlLogin|
|ACS URL|【サーバ名】/Saml2/Acs<br>https://sso-pleasanter.com/pleasanter/Saml2/Acs|

## 3. SAMLログインの実行

[Authentication.json](../../parameters/authentication-json.md)の編集が済んだら、IISを再起動してください。  
再起動後、ブラウザからアクセスするとログイン画面にSAML認証用のログインボタン（「SSOログイン」ボタン）が表示されます。このボタンをクリックし、SAML認証の動作確認を行ってください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.8.0 以降|NotCreatePersistentCookieを追加|
|1.2.6.0 以降|機能追加|

## 関連情報

-   [パラメータ設定：Authentication.json](../../parameters/authentication-json.md)
-   [FAQ：SAML認証で、ユーザー項目を「Name」の代わりに「givenName」と「surname」を結合して指定したい](../../../FAQ/system-requirements-and-setup/faq-saml-sync-user-item-name.md)  
-   [FAQ：SAML認証で、ユーザー項目の「DeptCode」を指定せずに組織に反映したい](../../../FAQ/system-requirements-and-setup/faq-saml-sync-user-item-dept.md)  
-   [FAQ：SAML認証設定でAuthentication.json に設定するSAMLレスポンスの属性名を確認したい](../../../FAQ/system-requirements-and-setup/faq-saml-response.md)
