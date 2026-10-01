---
title: SCIM機能
category: 追加設定：アカウント連携
order: '100'
status: ''
parts: ''
urlstring: scim
translationKey: scim
shortname: SCIM機能
created: 2026-08-13
updated: 2026-09-08
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/6461453c544b4368b1351071c396c953.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/944dcfcdcc204213a19205a5e0589d0a.svg#only-dark)](https://pleasanter.org/support/)

## 概要

SCIM（System for Cross-domain Identity Management）は、異なるシステムやクラウドサービス間で、ユーザ情報・グループ情報を自動で連携・管理するための標準規格（プロトコル）です。

SCIM機能を利用すると、Microsoft Entra ID（旧Azure AD）のようなIDプロバイダとプリザンターとの間で、ユーザ情報・グループ情報を自動連携・管理できます。

![IDプロバイダとプリザンターの間でユーザ情報・グループ情報を自動連携する仕組みの図](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/2f1ba61b640e43899d530cf33ceeb4e6.png)

### SAMLとの違い

ユーザ情報が受け渡しされるという点で、SCIMと[SAML認証](../../authn-authz/saml.md)は似ていますが、以下のような違いがあります。

|              | SAML                                                            | SCIM                                                                       |
| :----------- | :-------------------------------------------------------------- | :------------------------------------------------------------------------- |
| 役割         | 認証（シングルサインオン）                                      | IDプロビジョニング（自動連携）                                             |
| 目的         | 1回のログインでプリザンターを含む複数のサービスを利用可能にする | IDプロバイダとプリザンター間でユーザ情報を自動で作成・削除する             |
| タイミング   | ユーザがプリザンターにアクセスした瞬間に動作                    | 管理者がIDプロバイダでユーザを追加・変更・削除した時に動作                 |
| データの流れ | ユーザのブラウザを経由した一時的な認証情報の受け渡し            | IDプロバイダからプリザンターへのバックグラウンドでの永続的なデータ書き込み |

## 前提条件

1. 本機能の設定には、IDプロバイダ（Microsoft Entra ID）の管理権限が必要です。
1. 本機能の設定は、「[テナント管理者](../../../../managers-guide/user-administration/user-management-tenant-manager.md)」または「[特権ユーザ](../../../../managers-guide/user-administration/user-management-privileged-users.md)」が実施する必要があります。
1. SCIM機能の設定にあたり、IDプロバイダの送信元IPアドレスを把握しておく必要があります。

## 操作手順

SCIM機能をはじめて利用する場合は、以下の手順を実施してください。

| No. | 手順                     | 詳細                                                                                                                                                                                                                        |
| --: | :----------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|   1 | IPアドレス制御設定の確認 | [Security.json](../../../parameters/security-json.md)のパラメータ「AllowIpAddresses」の設定を確認してください。                                                                                                                                                   |
|   2 | SCIM機能の有効化         | [Scim.json](../../../parameters/scim-json.md)のパラメータ「Enabled」をtrueに設定してください。                                                                                                                                                                  |
|   3 | SCIMトークンの新規作成   | 「[テナントの管理](../../../../managers-guide/tenant-administration/index.md)」画面の「SCIMトークン」タブで、IDプロバイダからプリザンターへの接続で使用される認証情報を新規作成してください。<br>詳細は[プリザンターの初期設定](scim-pleasanter-setup.md)の「2. SCIMトークンの新規作成」を参照してください。 |
|   4 | IDプロバイダの設定     | プリザンターユーザマニュアルでは、IDプロバイダとしてMicrosoft Entra IDを用いた場合の設定方法を説明します。<br>詳細は[IDプロバイダの初期設定](scim-idp-setup.md)を参照してください。                                                  |
|   5 | プリザンターの連携設定 | IDプロバイダ側の設定情報を、プリザンター側の連携設定に反映します。<br>詳細は[Scim.json](../../../parameters/scim-json.md)の「ExtendedAttributes」の説明を参照してください。                                                                                 |

上記の手順完了後、カスタム属性の連携を設定したい場合は、以下の手順を実施してください。以下のマニュアルはプリザンターの設定とIDプロバイダの設定を含みます。

| No. | 手順                     | 詳細                                                                                                                                                                                                                        |
| --: | :----------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|   6 | カスタム属性の連携設定 | [カスタム属性の連携設定](scim-sync-custom-attributes.md)を参照してください。                                                                                                                                                   |

## トラブルシュート

テスト接続がうまくいかない場合や、エラーが表示される場合は、以下のFAQを参照してください。

-   [FAQ：SCIMでユーザ情報が連携されない](../../../../FAQ/system-administration-operations-and-settings/faq-scim-sync-failure.md)

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.5.8.0 以降   | 機能追加 |

## 関連情報

-   [SAML認証を利用する](../../authn-authz/saml.md)
-   [プリザンターの初期設定](scim-pleasanter-setup.md)
-   [IDプロバイダの初期設定](scim-idp-setup.md)
-   [カスタム属性の連携設定](scim-sync-custom-attributes.md)
-   [FAQ：SCIMでユーザ情報が連携されない](../../../../FAQ/system-administration-operations-and-settings/faq-scim-sync-failure.md)
