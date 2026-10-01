---
title: SAMLレスポンス内のユーザ情報をカスタム項目としてユーザ画面に取り込む
category: 追加設定：認証
order: '0'
status: ''
parts: ''
urlstring: saml-response-mapping
translationKey: saml-response-mapping
shortname: SAMLレスポンス内のユーザ情報をカスタム項目としてユーザ画面に取り込む
created: 2026-07-22
updated: 2026-08-12
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/d87dbd3bf35747068af635423b1ecc3a.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/7315fe8adc2840ee857e2644dac54878.svg#only-dark)](https://pleasanter.org/support/)

（本機能は[Extensionsトライアル](../../../products-info/extensions-trial/index.md)で試用可能です）

## 概要

[SAML認証](saml.md)でのログインに成功すると、SAMLレスポンスとして渡されるユーザデータを基に、プリザンターのユーザ情報を作成・更新できます。

本機能は[SAML認証](saml.md)の「SamlParameters.Attributes項目一覧」に記載されている項目以外の任意の項目を、「[拡張項目](../../../developers-guide/extended-features/extended-column.md)」を使って設置した項目へマッピングする機能です。

![SAMLレスポンスの項目をユーザ画面の拡張項目へマッピングする流れの図](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/26167701092b476c9dc38c32fa83bef1.png)

## 前提条件

1. [SAML認証](saml.md)でプリザンターにログインできることを確認してください。
1. [SAML認証](saml.md)のマニュアルで「ユーザ項目の同期について」を参照し、「SamlParameters.Attributes項目一覧」に記載されている項目が同期されることを確認してください。「生年月日」項目と「性別」項目の追加方法は、以下のFAQを参照してください。  
   [FAQ：ユーザの管理で生年月日と性別を表示したい](../../../FAQ/system-administration-operations-and-settings/faq-visible-user-birthday.md)

## 操作手順

#### 1. SAMLレスポンスの調査

SAMLレスポンスを確認し、本機能で追加すべき項目を把握してください。  
SAMLレスポンスの確認方法は、以下のFAQを参照してください。  
[FAQ：SAML認証設定でAuthentication.json に設定するSAMLレスポンスの属性名を確認したい](../../../FAQ/system-requirements-and-setup/faq-saml-response.md)

#### 2. 拡張項目の追加

「[拡張項目](../../../developers-guide/extended-features/extended-column.md)」を使い、「[ユーザ](../../../managers-guide/user-administration/index.md)」の管理画面に対して、必要な項目を追加してください。  
「[拡張項目](../../../developers-guide/extended-features/extended-column.md)」では、「分類」項目、「数値」項目、「説明」項目、「日付」項目、「チェック」項目を追加できます。

#### 3. Authentication.jsonの編集

[Authentication.json](../../parameters/authentication-json.md)のパラメータSamlParameters.Attributesを、「[拡張項目](../../../developers-guide/extended-features/extended-column.md)」で追加した項目に併せて編集してください。

#### 4. Webサーバの再起動とログイン

IISを再起動し、パラメータの変更を反映してください。SAML認証でのログインが成功すると、ユーザ情報の作成・更新が行われます。

## 関連情報

-   [SAML認証を利用する](saml.md)

