---
title: プリザンターの初期設定
category: 追加設定：アカウント連携
order: '200'
status: ''
parts: ''
urlstring: scim-pleasanter-setup
translationKey: scim-pleasanter-setup
shortname: プリザンターの初期設定
created: 2026-08-13
updated: 2026-09-08
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/6461453c544b4368b1351071c396c953.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/944dcfcdcc204213a19205a5e0589d0a.svg#only-dark)](https://pleasanter.org/support/)

## 概要

[SCIM機能](index.md)を利用するには、プリザンター側で以下の設定が必要です。

1. [Security.json](../../../parameters/security-json.md)のパラメータ「AllowIpAddresses」の設定を確認する
1. プリザンターでSCIMトークンを発行する

## 注意事項

1. SCIMトークンは、新規作成時に一度だけ画面表示されます。同じSCIMトークンを再表示することはできません。コピーして安全な場所に保管してください。
1. SCIM トークンは、IdP から Pleasanter のユーザー・グループ情報を更新できる重要な認証情報です。セキュリティの観点から以下の遵守を推奨します。
   1. トークンは必要な担当者だけが扱います。
   1. 発行されたトークンは安全な場所に保管します。
   1. 不要になったトークンは削除します。
   1. 漏えいの可能性がある場合は、該当トークンを削除し、新しいトークンを発行します。
   1. 有効期限を設定すると、期限切れ時に連携が停止するため、更新忘れに注意します。

## 前提条件

1. IDプロバイダの送信元IPアドレスを把握しておく必要があります。
1. [Scim.json](../../../parameters/scim-json.md)のパラメータ「Enabled」をtrueに設定してください。SCIM機能が有効化され、「[テナントの管理](../../../../managers-guide/tenant-administration/index.md)」画面に「SCIMトークン」タブが表示されます。
1. 「[テナント管理者](../../../../managers-guide/user-administration/user-management-tenant-manager.md)」または「[特権ユーザ](../../../../managers-guide/user-administration/user-management-privileged-users.md)」で設定してください。

## 操作手順

### 1.「Security.json」のパラメータ「AllowIpAddresses」の設定を確認する

IPアドレスによるアクセス制御を行っている場合、[Security.json](../../../parameters/security-json.md)のパラメータ「AllowIpAddresses」へ、IDプロバイダの送信元IPアドレスまたはCIDR表記を追加してください。プリザンターは、このパラメータに指定したIPアドレスからの接続のみを許可します。IDプロバイダ側の送信元IPアドレスがAllowIpAddressesに追加されていない場合、403 Forbiddenとなります。

##### 設定例

```json
{
    "AllowIpAddresses": [
        "203.0.113.10",
        "203.0.113.0/24"
    ]
}
```

なお、パラメータAllowIpAddressesの値がnullまたは空の場合、IPアドレスによるアクセス制御は行われません。

```json
{
    "AllowIpAddresses": null
}
```

### 2. SCIMトークンを新規作成する

SCIMトークンは、Microsoft Entra IDなどのIDプロバイダがプリザンターのSCIM APIに接続するための認証情報です。

SCIM機能を利用するには、プリザンターが発行するSCIMトークンをIDプロバイダへ登録する必要があります。

1. 「[テナント管理者](../../../../managers-guide/user-administration/user-management-tenant-manager.md)」または「[特権ユーザ](../../../../managers-guide/user-administration/user-management-privileged-users.md)」で「テナント管理」画面を開いてください。
1. 「SCIMトークン」タブを開き、「新規作成」ボタンをクリックしてください。

       ![「テナント管理」画面の「SCIMトークン」タブ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/8c8fdcaf8719413399af1e4c0e1cf1eb.png)

1. 「SCIMトークン」ダイアログが表示されます。「有効期限」を設定し、「追加」ボタンをクリックしてください。

       ![「SCIMトークン」ダイアログ。有効期限を設定して「追加」ボタンを押す](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/0db097ff18a945a4965327c1d9a27de7.png)

       | 項目     | 内容                                                                                     |
       | -------- | ---------------------------------------------------------------------------------------- |
       | 有効期限 | トークンの有効期限を日時指定します。空の場合、当該トークンは無期限で使用可能となります。 |
       | 無効     | オンにすると、当該トークンを使用できなくなります。                                       |

1. 画面にSCIMトークンが**一度だけ表示**されます。SCIMトークンはIDプロバイダへ登録する必要があります。コピーして安全な場所に保管してください。

       ![発行されたSCIMトークンが一度だけ表示された画面](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/f16534b8732d47a283cda314fcf61b19.png)

1. SCIMトークンのコピーが済んだら、ダイアログ右上の閉じる（［×］）ボタンをクリックしてください。「SCIMトークン」タブに戻ります。  
   「SCIMトークン」タブでは、以下の情報を確認できます。SCIMトークンそのものは表示されません。

   ![「SCIMトークン」タブのトークン一覧。トークンそのものは表示されない](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/a213d9babddc4f83b29ba68424ec8f57.png)

   | 項目             | 内容                           |
   | ---------------- | ------------------------------ |
   | ID               | プリザンター内部のトークンID   |
   | トークン先頭文字 | トークンの先頭部分             |
   | 作成者           | トークンを作成したユーザ       |
   | 無効             | トークンが無効かどうか         |
   | 有効期限         | トークンの有効期限             |
   | 最終使用日時     | SCIM APIで最後に使用された日時 |
   | 作成日時         | トークンを作成した日時         |

### IDプロバイダに設定する値

Microsoft Entra IDなどのIDプロバイダ側では、SCIM設定に以下の情報を指定する必要があります。SCIMトークンは認証方式「Bearer」を付けずに、作成された値をそのまま設定してください。

| 項目      | 設定する値                            |
| --------- | ------------------------------------- |
| 接続先URL | https://{{プリザンターのURL}}/scim/v2 |
| 認証方式  | Bearer Token（OAuth 2.0）             |
| Token     | 新規作成したSCIMトークン              |

### 3. SCIMトークンの有効期限を変更する

作成済みのSCIMトークンの有効期限を変更できます。

1. 「SCIMトークン」タブのSCIMトークン一覧で、変更したいSCIMトークンをクリックしてください。
1. 以下の画面が表示されるので、有効期限を変更し、「変更」ボタンをクリックしてください。

       ![SCIMトークンの編集画面。有効期限を変更する](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/b1d2a00b52974af186e7fb39cadfe37d.png)

1. コマンドボタンエリアの「更新」ボタンをクリックしてください。

### 4. SCIMトークンを無効化する

IDプロバイダ側の設定を維持したまま、一時的に接続を停止したい場合は、IDプロバイダとの接続に使用しているSCIMトークンを無効化してください。SCIMトークンを無効化すると、プリザンターSCIM APIの認証に失敗します。

1. 「SCIMトークン」タブのSCIMトークン一覧で、変更したいSCIMトークンをクリックしてください。
1. 以下の画面が表示されるので、「無効」をクリックしてオンにします。

       ![SCIMトークンの編集画面。「無効」をオンにする](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/4224cf84878c4653aa371f24d371bed2.png)

1. コマンドボタンエリアの「更新」ボタンをクリックしてください。

### 5. トークンを削除する

不要になったSCIMトークンは削除することができます。削除したトークンは使用できなくなります。

1. 「SCIMトークン」タブのSCIMトークン一覧で、変更したいSCIMトークンの左端にあるチェックボックスをクリックしてオンにしてください。
1. 「削除」ボタンをクリックしてください。

IDプロバイダに、プリザンターで削除済みのSCIMトークンが登録されたままの場合、SCIM連携は認証エラーになります。

### 6. SCIMトークンの再発行

SCIMトークンの再発行は、以下の流れで実施してください。古いトークンを先に削除すると、IDプロバイダの設定を差し替えるまでSCIM連携が失敗します。

1. 「テナント管理」画面の「SCIMトークン」タブでSCIMトークンを新規作成してください。
1. （Microsoft Entra IDなどの）IDプロバイダ側で、古いSCIMトークンを新しいSCIMトークンに差し替えてください。
1. IDプロバイダ側で接続テストまたは連携確認を行ってください。
1. 問題がなければ、プリザンターから古いSCIMトークンを削除してください。

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.5.8.0 以降   | 機能追加 |

## 関連情報

-   [SCIM機能](index.md)
-   [IDプロバイダの初期設定](scim-idp-setup.md)
-   [FAQ：SCIMでユーザ情報が連携されない](../../../../FAQ/system-administration-operations-and-settings/faq-scim-sync-failure.md)