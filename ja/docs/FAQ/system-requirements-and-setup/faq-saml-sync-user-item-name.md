---
title: SAML認証で、ユーザー項目を「Name」の代わりに「givenName」と「surname」を結合して指定したい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-saml-sync-user-item-name
translationKey: faq-saml-sync-user-item-name
shortname: ''
created: 2025-07-14
updated: 2025-09-24
---

## 回答

"Attributes": "Name"が空の場合、"Attributes": "FirstName"に"givenName"、"Attributes": "LastName"に"givenName"を設定することで、"LastName"と"FirstName"で取得した値をもとに"Name"を作成できます。

---

## 概要

[SAML認証](../../setup/additional/authn-authz/saml.md)で"Attributes": "Name"がnullの場合、"LastName"と"FirstName"で取得した値をもとに「Name」を作成します。

そのため、以下のように記述すると、"givenName"と"surname"で"Name"を指定できます。

``` json title="Authentication.json" linenums="1" hl_lines="3-5"
    "SamlParameters": {
        "Attributes": {
            "Name": null,
            "FirstName": "givenName",
            "LastName": "surname",
                : 中略
        }
    }
```

## 「名前」に設定する属性名の指定方法

"FirstName"と"LastName"の項目を追加している場合、"Name"にnullを指定し、ユーザ項目名に"FirstName"と"LastName"に追加することで、"FirstName"と"LastName"を組み合わせた値を"Name"に設定できます。

指定したSAML属性から値が取得できなかった場合、ログインIDが設定されます。

=== "設定例　名前にNameを利用する場合"

    ``` json title="Authentication.json" linenums="1" hl_lines="3-5"
        "SamlParameters": {
            "Attributes": {
                "Name": "Name",
                "UserCode": "UserCode",
                "Birthday": "Birthday",
                    : 中略
            }
        }
    ```

=== "設定例　名前にFirstNameとLastNameを組み合わせた値を利用する場合"

    Nameにはnullを指定します。

    ``` json title="Authentication.json" linenums="1" hl_lines="3-5"
        "SamlParameters": {
            "Attributes": {
                "Name": null,
                "FirstName": "FirstName",
                "LastName": "LastName",
                "UserCode": "UserCode",
                "Birthday": "Birthday",
                    : 中略
            }
        }
    ```

## 関連情報

-   [SAML認証を利用する](../../setup/additional/authn-authz/saml.md)
