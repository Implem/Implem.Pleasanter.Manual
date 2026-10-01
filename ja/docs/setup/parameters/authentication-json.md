---
title: Authentication.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: authentication-json
translationKey: authentication-json
shortname: Authentication.json
created: 2019-04-30
updated: 2026-04-15
---

## 注意事項

-   パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 制限事項

-   グループの同期はLinux環境では利用できません。Windows環境で"DsProvider"に"Novell"を指定した場合も利用できません。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

### トップレベルパラメータ

| パラメータ名           | 設定例                                                | 説明                                                                                                                                                                                                                                                                                                                                         |
| :--------------------- | :---------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Provider               | null<br>"LDAP"<br>"LDAP+Local"<br>"Windows"<br>"SAML" | **（LDAP認証の場合は必須）**<br><br>null<br>ローカルユーザによる認証を利用。<br><br>"LDAP"<br>ADなどの外部LDAP認証を利用。<br><br>"LDAP+Local"<br>LDAP認証でログインに失敗した場合、ローカルユーザによるログインを試行。<br><br>"Windows"<br>[統合Windows認証](../additional/authn-authz/active-directory-sso.md)を利用。<br><br>"SAML"<br>[SAML認証](../additional/authn-authz/saml.md)を利用。 |
| DsProvider             | null<br>（デフォルト値）                              | "Novell"<br>Windows環境において、LDAP認証ライブラリとして明示的にNovell.Directory.Ldapを利用（Linux環境ではNovellのみ指定可能）。                                                                                                                                                                                                            |
| ServiceId              | null                                                  | 変更不可。                                                                                                                                                                                                                                                                                                                                   |
| ExtensionUrl           | null                                                  | 変更不可。                                                                                                                                                                                                                                                                                                                                   |
| RejectUnregisteredUser | true                                                  | true<br>プリザンターに登録されていないユーザによるログインを拒否。<br><br>false<br>LDAP認証を行っている場合、認証されたユーザを自動的にプリザンターに登録。                                                                                                                                                                                  |
| PasskeyParameters      | JSONオブジェクト                                      | [パスキー認証](../additional/authn-authz/passkey.md)を参照。                                                                                                                                                                                                                                                                        |
| LdapParameters         | JSON配列                                              | LDAP認証に必要な詳細設定。JSON配列として複数のLDAPサーバを指定可能。ローカル認証の場合は設定不要。以下の[LdapParameters配下のパラメータ](#ldapparameters)を参照。                                                                                                                                                                            |
| SamlParameters         | JSONオブジェクト                                      | [SAML認証](../additional/authn-authz/saml.md)を参照。                                                                                                                                                                                                                                                                               |
| TrustedProxyParameters | JSONオブジェクト                                      | リバースプロキシが付与するHTTPヘッダーを使ってユーザを自動ログインさせる信頼済みリバースプロキシ認証の設定。本パラメータの設定例については[信頼済みリバースプロキシ認証](../additional/authn-authz/trusted-reverse-proxy-auth.md)を参照。                                                                                           |

### LdapParameters配下のパラメータ

| パラメータ名                | 設定例                                         | 説明                                                                                                                                                                                                                |
| :-------------------------- | :--------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| LdapSearchRoot              | "LDAP://dc.example.local/dc=example,dc=local"  | **（LDAP認証の場合は必須）**<br><br>LDAPの検索開始位置を指定。LDAPは**大文字**で記載。                                                                                                                              |
| LdapSearchProperty          | "sAMAccountName"                               | **（LDAP認証の場合は必須）**<br><br>ログイン名に使用する属性の名称。                                                                                                                                                |
| LdapSearchPattern           | (&(account={loginId})(deptcode=12345))         | ログイン後のログインユーザ情報取得時の検索パターン。複数部署に所属するユーザから特定部署に絞るなど"SearchProperty=loginId"で取得できない場合に対応できる。                                                          |
| LdapLoginPattern            | null                                           | LDAPサーバへのログインアカウントのパターンを設定します。OpenLDAPでのuid=xx,ou=xx,o=xx,c=xxの形式に対応できます。<br><br>null<br>uid={loginId},ou=people,o=example,c=comの{loginId}に入力アカウントをReplaceします。 |
| LdapAuthenticationType      | null                                           | SASL非対応のサーバに対応します。nullの場合はSimple認証。                                                                                                                                                            |
| NetBiosDomainName           | "EXAMPLE"                                      | **（Windows認証でSSOする場合は必須）**<br><br>ドメインのNetBios名を**大文字**で記載。                                                                                                                               |
| LdapTenantId                | 1                                              | 変更不可。                                                                                                                                                                                                          |
| LdapDeptCode                | "departmentNumber"                             | 組織コードに使用する属性の名称。                                                                                                                                                                                    |
| LdapDeptCodePattern         | null                                           | 組織コードの文字の一部を取得する正規表現。 [^1]                                                                                                                                                                     |
| LdapDeptName                | "department"                                   | 組織名に使用する属性の名称。                                                                                                                                                                                        |
| LdapDeptNamePattern         | null                                           | 組織名の文字の一部を取得する正規表現。 [^1]                                                                                                                                                                         |
| LdapUserCode                | "employeeNumber"                               | ユーザコードに使用する属性の名称。                                                                                                                                                                                  |
| LdapUserCodePattern         | null                                           | ユーザコードの文字の一部を取得する正規表現。 [^1]                                                                                                                                                                   |
| LdapFirstName               | "givenName"                                    | ファーストネームに使用する属性の名称。                                                                                                                                                                              |
| LdapFirstNamePattern        | null                                           | ファーストネームの文字の一部を取得する正規表現。 [^1]                                                                                                                                                               |
| LdapLastName                | "sn"                                           | ラストネームに使用する属性の名称。                                                                                                                                                                                  |
| LdapLastNamePattern         | null                                           | ラストネームの文字の一部を取得する正規表現。 [^1]                                                                                                                                                                   |
| LdapMailAddress             | "mail"                                         | ユーザのメールアドレスに使用する属性の名称。                                                                                                                                                                        |
| LdapMailAddressPattern      | null                                           | ユーザのメールアドレスの文字の一部を取得する正規表現。 [^1]                                                                                                                                                         |
| LdapExtendedAttributes      | JSON配列                                       | 以下の3パラメータ（Name、Pattern、ColumnName）を1レコードとした配列として格納。複数の項目を指定することが可能。以下に記載例を掲載。 [^2]                                                                            |
| Name                        | "DisplayName"                                  | 追加取得する属性の名称。                                                                                                                                                                                            |
| Pattern                     | null                                           | 追加取得する文字の一部を取得する正規表現。 [^1]                                                                                                                                                                     |
| ColumnName                  | "ClassA"                                       | 追加取得する値を格納するプリザンターのUsersテーブル項目名。                                                                                                                                                         |
| LdapGroupName               | "cn"                                           | グループ名に使用する属性の名称。                                                                                                                                                                                    |
| LdapGroupNamePattern        | null                                           | グループ名の文字の一部を取得する正規表現。 [^1]                                                                                                                                                                     |
| LdapSyncPageSize            | 0                                              | LdapSyncの際にPageSizeの変更に対応。<br><br>-1<br>PageSizeを指定できないサーバの場合。<br><br>0または項目を省略<br>既定値1000となる。                                                                               |
| LdapSyncPatterns            | "(&(ObjectCategory=User)(ObjectClass=Person))" | ユーザを検索するための検索パターン。 [^3]                                                                                                                                                                           |
| LdapSyncGroupPatterns       | "(&(ObjectCategory=Group))"                    | グループを検索するための検索パターン。 [^3]                                                                                                                                                                         |
| LdapGroupExtendedAttributes | JSON配列                                       | 以下の3パラメータ（Name、Pattern、ColumnName）を1レコードとした配列として格納。複数の項目を指定することが可能。以下に記載例を掲載。 [^2]                                                                            |
| Name                        | "DisplayName"                                  | 追加取得する属性の名称。                                                                                                                                                                                            |
| Pattern                     | null                                           | 追加取得する文字の一部を取得する正規表現。 [^1]                                                                                                                                                                     |
| ColumnName                  | "ClassA"                                       | 追加取得する値を格納するプリザンターのGroupsテーブル項目名。                                                                                                                                                        |
| LdapExcludeAccountDisabled  | true                                           | 無効化されたユーザを取り込まないためのフラグ。                                                                                                                                                                      |
| AutoDisable                 | true                                           | LDAPで認証対象外となったアカウントについて、プリザンターのユーザ情報に無効化を反映するためのフラグ。                                                                                                                |
| AutoEnable                  | true                                           | LDAPで認証対象となったアカウントについて、プリザンターのユーザ情報に有効化を反映するためのフラグ。                                                                                                                  |
| LdapSyncUser                | "DomainUserName"                               | LDAPとユーザ同期を行う際に使用するユーザ名。<br><br>Linux<br>ドメインを含むユーザログオン名を指定する。<br>例：hayato@implem.local<br><br>Windows<br>ドメイン名の指定は不要。                                       |
| LdapSyncPassword            | "\*\*\*\*\*\*\*\*"                             | LDAPとユーザ同期を行う際に使用するユーザのパスワード。                                                                                                                                                              |

[^1]:
    正規表現に一致する最初の文字列が使用されます。nullの場合は文字列全体が使用されます。

[^2]:
    以下のAPIのレスポンスに該当カラムを含めたい場合は、「[拡張機能：拡張項目](../../developers-guide/extended-features/extended-column.md)」に、パラメータ "GridEnabled"と"EditorEnabled"のどちらか一方または両方に"1"を指定したカラムを追加してください。

    1.  [API：ユーザ操作：ユーザ取得](../../developers-guide/api/user-operations/api-user-get-all.md)
    1.  [API：グループ操作：グループ取得](../../developers-guide/api/group-operations/api-group-get.md)

[^3]:
    検索パターンは[マイクロソフト社のリファレンス](https://technet.microsoft.com/ja-jp/library/security/system.directoryservices.directorysearcher.filter(v=vs.85)?cs-save-lang=1&cs-lang=vb)に従って記述してください。  

### LdapExtendedAttributesとLdapGroupExtendedAttributesの記載例

以下は、LdapExtendedAttributesの記載例です。LdapGroupExtendedAttributesも同様に記載できます。

``` json linenums="1"
            "LdapExtendedAttributes": [
                {
                    "Name": "DisplayName",
                    "Pattern": null,
                    "ColumnName": "DescriptionE"
                }
            ]
```

### 正規表現の記載例

LDAPサーバ側の"department"に「12345 総務部」と登録されているケースにおいて、「総務部」を抽出する例です。

``` json linenums="1"
            "LdapDeptName": "department",
            "LdapDeptNamePattern": "(?<=^.{6}).*",
```

## 対応バージョン

| 対応バージョン | 内容                              |
| :------------- | :-------------------------------- |
| 1.4.11.0以降   | LdapGroupExtendedAttributesを追加 |
| 1.5.1.0以降    | PasskeyParametersを追加           |
| 1.5.3.0以降    | TrustedProxyParametersを追加      |

## 関連情報

-   [パラメータ変更時の確認事項](parameter-edit.md)
-   [パスキー認証](../additional/authn-authz/passkey.md)
-   [SAML認証](../additional/authn-authz/saml.md)
-   [信頼済みリバースプロキシ認証](../additional/authn-authz/trusted-reverse-proxy-auth.md)
