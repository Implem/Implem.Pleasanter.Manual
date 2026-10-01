---
title: LDAP認証を利用する
category: 追加設定：認証
order: '400'
status: ''
parts: ''
urlstring: ldap
shortname: LDAP認証
created: 2026-08-18
updated: 2026-09-08
---

## 概要

所属組織のユーザ認証基盤としてActive DirectoryなどのLDAPサーバを利用できる場合、プリザンターのユーザ認証をLDAPサーバで行えます。LDAP認証を設定している場合、プリザンターは下図の1.～3.のように動作します。

![LDAP認証時のプリザンターとLDAPサーバ間の動作の流れ（1～3）](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/39c98395e89d4a908aaaea5b5eb2c872.png)

一般的に、LDAPサーバはイントラネット内に存在するため、LDAPサーバを利用して認証を行う場合はプリザンターをイントラネットに構築する必要があります。

### LDAP認証の設定

LDAP認証を行うには、[Authentication.json](../../parameters/authentication-json.md)を例えば以下のように設定してください。

```json
{
    "Provider": "LDAP",
    "DsProvider": null,
    "ServiceId": null,
    "ExtensionUrl": null,
    "RejectUnregisteredUser": false,
    "LdapParameters": [
        {
            "LdapSearchRoot": "LDAP://ldap.example.local/ou=Company,dc=example,dc=local",
            "LdapSearchProperty": "sAMAccountName",
            "LdapSearchPattern": null,
            "LdapLoginPattern": null,
            "LdapAuthenticationType": null,
            "NetBiosDomainName": "EXAMPLE",
            "LdapTenantId": 1,
            "LdapDeptCode": "Company",
            "LdapDeptCodePattern": null,
            "LdapDeptName": "department",
            "LdapDeptNamePattern": null,
            "LdapUserCode": null,
            "LdapUserCodePattern": null,
            "LdapFirstName": "givenName",
            "LdapFirstNamePattern": null,
            "LdapLastName": "sn",
            "LdapLastNamePattern": null,
            "LdapMailAddress": "mail",
            "LdapMailAddressPattern": null,
            "LdapGroupName": "cn",
            "LdapGroupNamePattern": null,
            "LdapSyncPageSize": 0,
            "LdapSyncPatterns": [
                "(&(ObjectCategory=User)(ObjectClass=Person))"
            ],
            "LdapSyncGroupPatterns": [
                "(&(ObjectCategory=Group))"
            ]
            "LdapExcludeAccountDisabled": false,
            "AutoDisable": false,
            "AutoEnable": false,
            "LdapSyncUser": "Administrator",
            "LdapSyncPassword": "********"
        }
    ],

～～ 中略 ～～

}
```

### ローカル認証とLDAP認証の併用

[Authentication.json](../../parameters/authentication-json.md)のパラメータ「Provider」の値が「LDAP+Local」に設定されている場合、LDAP認証を試みた後にローカル認証を試みます。これにより、LDAPサーバに登録されていないユーザをローカルユーザとして登録し、両方の方式でユーザ認証を行えます。

###  プリザンターとLDAPサーバ間の暗号化

プリザンターとLDAPサーバ間の通信がLDAPを使用して行われる場合、入力されたログインIDとパスワードが平文で送信されます。通信内容を暗号化するには、LDAPS を使用してください。LDAPSを使用するには、[Authentication.json](../../parameters/authentication-json.md)のパラメータ「LdapSearchRoot」を以下のように設定します。

```json
{

～～ 中略 ～～

    "LdapParameters": [
        {
            "LdapSearchRoot": "LDAPS://ldap.example.local:636/ou=Company,dc=example,dc=local",

～～ 中略 ～～

        }
    ],

～～ 中略 ～～

}
```
