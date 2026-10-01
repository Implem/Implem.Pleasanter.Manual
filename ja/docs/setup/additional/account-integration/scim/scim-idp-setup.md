---
title: IDプロバイダの初期設定
category: 追加設定：アカウント連携
order: '300'
status: ''
parts: ''
urlstring: scim-idp-setup
translationKey: scim-idp-setup
shortname: IDプロバイダの初期設定
created: 2026-08-13
updated: 2026-09-08
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/6461453c544b4368b1351071c396c953.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/944dcfcdcc204213a19205a5e0589d0a.svg#only-dark)](https://pleasanter.org/support/)

## 概要

[SCIM機能](index.md)を利用するには、IDプロバイダ側で以下の初期設定が必要です。

以下では、IDプロバイダとしてMicrosoft Entra IDを用いる場合を例に、具体的な初期設定の手順を紹介します。

1. 準備
1. エンタープライズ アプリケーションの作成
1. プロビジョニングの構成
1. ユーザの「属性マッピング」設定
1. グループの「属性マッピング」設定

## 注意事項

1. 連携方向は、IDプロバイダからプリザンターへの一方向のみです。プリザンター側で変更したユーザ情報やグループ情報は、IDプロバイダ側へ連携されません。
1. 連携されたユーザ情報やグループ情報をプリザンター側で変更した場合、次回以降の連携により、IDプロバイダ側が送信する情報で上書きされる可能性があります。

## 前提事項

1. [SCIM機能](index.md)を参照し、SCIM機能を有効化してください。

## 操作手順

以下は、Microsoft Entra IDからプリザンターへ、ユーザ情報とグループ情報を連携する設定手順です。

### 1. 準備

以下の情報を準備してください。

| 項目                         | 内容                                                             |
| :--------------------------- | :--------------------------------------------------------------- |
| 接続先URL                    | プリザンターのSCIM APIのURL（【例】https://example.com/scim/v2） |
| SCIMトークン                 | プリザンターの「[テナントの管理](../../../../managers-guide/tenant-administration/index.md)」画面で発行したトークン。発行手順は[プリザンターの初期設定](scim-pleasanter-setup.md)の「2. SCIMトークンの新規作成」を参照 |
| Microsoft Entra IDの管理権限 | エンタープライズ アプリケーションを作成・編集できる権限          |

### 2. エンタープライズ アプリケーションの作成

ユーザ・グループ情報を送信するアプリケーションを作成します。「Microsoft Entra 管理センター」を開き、以下の手順を実施してください。

1. 画面左側のメニューから「エンタープライズ アプリ」を選択し、「新しいアプリケーション」を選択してください。
1. 「独自のアプリケーションの作成」を選択してください。
1. 「アプリケーションの名前」を入力してください。以下の画面では「Pleasanter SCIM」と入力しています。
1. 「ギャラリーに見つからないその他のアプリケーションを統合します」を選択してください。
1. 「作成」ボタンをクリックしてください。

![Microsoft Entra IDの独自アプリケーション作成画面。名前に「Pleasanter SCIM」を入力する](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/f912cffd24ee4854841041a6d87d536f.png)

### 3. プロビジョニングの構成

作成したエンタープライズ アプリケーションからプリザンターへの接続を設定します。作成したエンタープライズ アプリケーションを開き、以下の手順を実施してください。

1. 画面左側のメニューから「プロビジョニング」を選択してください。
1. 「新しい構成」を選択してください。
1. 「新しいプロビジョニング構成」画面へ、下表を参考にして、上記「1. 準備」で準備した情報を入力してください。

   | 項目                  | 入力値                             |
   | :-------------------- | :--------------------------------- |
   | テナントの URL        | プリザンターの接続先URL            |
   | シークレット トークン | プリザンターで発行したSCIMトークン |

1. 「テスト接続」ボタンをクリックしてください。
1. テスト接続が成功したら、「作成」ボタンをクリックしてください。

![「新しいプロビジョニング構成」画面。テナントのURLとシークレット トークンを入力する](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/c93c74a4f624470bbf0a38145e3e8b9d.png)

| ⚠ 接続テストに失敗する場合                                                                                                                                                                                                                                                                       |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 接続テストに失敗する場合は、以下の点を確認してください。<br><br>① SCIM機能を有効化している<br>② 接続先URLが正しい<br>③ SCIMトークンが正しい<br>④ SCIMトークンが有効（無効または期限切れになっていない）<br>⑤ IPアドレス制限の接続許可リストにMicrosoft Entra IDの送信元IPアドレスが設定されている |

### 4. ユーザの「属性マッピング」設定

ユーザの「属性マッピング」を確認・設定します。「属性マッピング」はMicrosoft Entra ID内のユーザ・グループ情報とプリザンターの項目とを紐づける設定です。

1. 「プロビジョニング」を開いてください。
1. 「マッピング」を開いてください。
1. 「Provision Microsoft Entra ID Users」を選択してください。

##### 「属性マッピング」画面

![「Provision Microsoft Entra ID Users」の「属性マッピング」画面](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/48d5574c64f44d858d04e3d3011dca7c.png)

#### 4.1 externalIdのマッピング

ユーザの照合には、Microsoft Entra ID 属性「objectId」を使用します。

既定では「userName」の「照合の優先順位」が「1」に設定されています（上記「属性マッピング」画面を参照）。そのため、最初に設定するときはobjectIdとマッピングする「externalId」の「照合の優先順位」を「2」に設定する必要があります。以下の手順を実施してください。

1. customappsso 属性が「externalId」の行の「編集」ボタンをクリックしてください。
1. 「属性の編集」画面が表示されます。以下のように設定してください。既定の「ソース属性」が「mailNickname」に設定されている場合は、必ず「objectId」に変更してください。

   | 項目                                     | 設定値     |
   | ---------------------------------------- | ---------- |
   | ソース属性（送信元）                     | objectId   |
   | 対象の属性（送信先）                     | externalId |
   | この属性を使用してオブジェクトを照合する | はい       |
   | 照合の優先順位                           | 2          |

1. 変更を保存します。「OK」ボタンをクリックしてください。

![externalIdの「属性の編集」画面。ソース属性objectId、照合の優先順位2を設定](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/8d216f6c240146c98a6ced676ded3f3d.png)

#### 4.2 userNameの照合を無効化する

userNameの照合を無効化することで、externalIdが唯一の照合属性となるように設定を変更します。

1. customappsso 属性が「userName」の行の「編集」ボタンをクリックしてください。
1. 「属性の編集」画面が表示されます。以下のように設定してください。

   | 項目                                     | 設定値            |
   | ---------------------------------------- | ----------------- |
   | ソース属性                               | userPrincipalName |
   | 対象の属性                               | userName          |
   | この属性を使用してオブジェクトを照合する | いいえ            |

1. 変更を保存します。「OK」ボタンをクリックしてください。

![userNameの「属性の編集」画面。照合に使用しない設定にする](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/b9f803beec804442a97f339e588253f3.png)

なお、userNameは、プリザンターの「ログインID」として連携されますので、「削除」しないでください。

#### 4.3 主なユーザ情報のマッピング例

主なユーザ情報のマッピング例を、以下にまとめます。

| Microsoft Entra ID 属性 | customappsso 属性                                                         | プリザンターの保存先 |
| ----------------------- | ------------------------------------------------------------------------- | -------------------- |
| objectId                | externalId                                                                | Users.ScimExternalId |
| userPrincipalName       | userName                                                                  | ログインID           |
| displayName             | displayName                                                               | ユーザ名             |
| givenName               | name.givenName                                                            | 名                   |
| surname                 | name.familyName                                                           | 姓                   |
| mail                    | emails[type eq "work"].value                                              | メールアドレス       |
| department              | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department     | 組織                 |
| employeeId              | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | ユーザコード         |
| manager                 | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager        | 上長                 |

プリザンター側で利用しない属性は、マッピングを無効化すれば連携されません。

マッピングの編集が済んだら、「属性マッピング」画面左上の「保存」をクリックしてください。

### 5. グループの「属性マッピング」設定

グループの「属性マッピング」を確認・設定します。

1. 「プロビジョニング」を開いてください。
1. 「マッピング」を開いてください。
1. 「Provision Microsoft Entra ID Groups」を選択してください。

![「Provision Microsoft Entra ID Groups」の「属性マッピング」画面](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/e88b51674364415d81a3997657f4d818.png)

#### 5.1 externalIdのマッピング

グループの照合にも、Microsoft Entra ID 属性の「objectId」を使用します。

1. 同じ名前のグループがプリザンターに存在していても、objectIdと紐づける「externalId」が異なる場合は、別のグループとして連携されます。
1. Azure ADのセキュリティ グループの入れ子構成も連携の対象です。

既定では「displayName」の「照合の優先順位」が「1」に設定されています。
そのため、最初に設定するときはobjectIdとマッピングする「externalId」の「照合の優先順位」を「2」に設定する必要があります。以下の手順を実施してください。

1. customappsso 属性が「externalId」の行の「編集」ボタンをクリックしてください。
1. 「属性の編集」画面が表示されます。以下のように設定してください。

   | 項目                                     | 設定値     |
   | ---------------------------------------- | ---------- |
   | ソース属性                               | objectId   |
   | ターゲット属性                           | externalId |
   | この属性を使用してオブジェクトを照合する | はい       |
   | 照合の優先順位                           | 2          |

1. 変更を保存します。「OK」ボタンをクリックしてください。

![グループのexternalIdの「属性の編集」画面。objectIdを照合に使う設定](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/0fb1d6a0d0e84baaad758cb1911083be.png)

#### 5.2 displayNameの照合を無効化する

displayNameの照合を無効化することで、externalIdが唯一の照合属性となるように設定を変更します。

1. customappsso 属性が「displayName」の行の「編集」ボタンをクリックしてください。
1. 「属性の編集」画面が表示されます。以下のように設定してください。

   | 項目                                     | 設定値      |
   | ---------------------------------------- | ----------- |
   | ソース属性                               | displayName |
   | ターゲット属性                           | displayName |
   | この属性を使用してオブジェクトを照合する | いいえ      |

![displayNameの「属性の編集」画面。照合に使用しない設定にする](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/4b5b8b303fe2443ab85167ebccdc42e2.png)

#### 5.3 主なグループ情報のマッピング例

主なグループ情報のマッピング例を、以下にまとめます。

| Microsoft Entra ID 属性 | customappsso 属性 | プリザンター の保存先 |
| ----------------------- | ----------------- | --------------------- |
| objectId                | externalId        | Groups.ScimExternalId |
| displayName             | displayName       | グループ名            |
| members                 | members           | グループメンバー      |

マッピングの編集が済んだら、「属性マッピング」画面左上の「保存」をクリックしてください。

### 6. 連携対象のユーザとグループを割り当てる

プロビジョニングの対象にするユーザまたはグループを、エンタープライズ アプリケーションに割り当てます。**初めて連携する場合は、少数のユーザーまたはグループだけを割り当てることを推奨**します。

1. 作成したエンタープライズ アプリケーションを開いてください。
1. 画面左側のメニューから「ユーザーとグループ」を開いてください。

   ![エンタープライズ アプリケーションの「ユーザーとグループ」画面](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/d65eb86bcf0845b18f793d9a90712540.png)

1. 「ユーザーまたはグループの追加」を選択してください。
1. 連携したいユーザーまたはグループを選択してください。
1. 「割り当て」ボタンをクリックしてください。

### 7. オンデマンドでプロビジョニングする

全体連携を開始する前に、1件ずつ連携できるか確認します。

1. 作成した「エンタープライズ アプリケーション」を開いてください。
1. 「プロビジョニング」を開いてください。
1. 「オンデマンドでプロビジョニング」を選択してください。
1. 連携するユーザーまたはグループを検索して、選択してください。検索には名前、usePrincipalName、メールアドレスを使用できます。

   ![「オンデマンドでプロビジョニング」で対象のユーザーやグループを検索する画面](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/c42f0b9eaca848878ef6b4ddd5d1f43f.png)

1. 「プロビジョニング」ボタンをクリックしてください。
1. プロビジョニングに成功すると、プリザンター側にユーザ情報またはグループ情報が連携されます。オンデマンドプロビジョニングが正しく実行されたかどうかは、以下を確認することで確かめられます。

   1. ユーザーが作成されている
   1. ログイン ID、氏名、メールアドレスが連携されている
   1. 組織が設定されている
   1. ユーザーコードが設定されている
   1. 上長が設定されている

### 8. プロビジョニングを開始する

オンデマンドプロビジョニングでの確認が済んだら、プロビジョニングを開始します。Microsoft Entra IDのプロビジョニングは、Microsoft Entra ID側のタイミングで実行されます。設定が済んでも、すぐには連携が開始されない可能性があります。結果をすぐに確認したい場合は、「オンデマンドでプロビジョニング」を実行してください。

1. 「プロビジョニング」を開いてください。
1. 「プロビジョニングの開始」をクリックしてください。

   ![「プロビジョニング」画面。「プロビジョニングの開始」を選ぶ](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/b55457f03eb84cbaa0dbac51161a7733.png)

### 9. 連携結果を確認する

連携後、プリザンター側で以下の内容を確認してください。

#### ユーザの連携結果を確認する

1. 対象ユーザ情報が作成または更新されている
1. ログインIDが正しく設定されている
1. 氏名、メールアドレスが連携されている
1. 組織、ユーザーコード、上長が連携されている
1. Microsoft Entra ID側で無効にしたユーザが、プリザンター側でも無効になる

#### グループの連携結果を確認する

1. 対象グループ情報が作成または更新されている
1. グループ名が連携されている
1. グループメンバーが連携されている
1. Azure ADのセキュリティグループの入れ子構成が連携されている

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.5.8.0 以降   | 機能追加 |

## 関連情報

-   [SCIM機能](index.md)
-   [プリザンターの初期設定](scim-pleasanter-setup.md)
-   [FAQ：SCIMでユーザ情報が連携されない](../../../../FAQ/system-administration-operations-and-settings/faq-scim-sync-failure.md)
