---
title: ASP.NET Coreデータ保護キーを外部保存する
category: 追加設定：クラスタ化への備え
order: '0'
status: ''
parts: ''
urlstring: data-protection-key-store
translationKey: data-protection-key-store
shortname: ASP.NET Coreデータ保護キーを外部保存する
created: 2026-07-16
updated: 2026-08-12
---

## 1. 概要

ASP.NET Coreは、認証CookieやCSRFトークンなどの保護対象データを、Data Protectionという仕組みで暗号化・復号します。

Data Protectionは既定で、各インスタンスのローカルにデータ保護キーを保持します。この場合、クラスタ構成で複数インスタンスを稼働させると、あるインスタンスが発行した認証Cookieを別のインスタンスで復号できません。データ保護キーを外部の共有可能な場所に保存し、すべてのインスタンスから参照できるようにする必要があります。

[Security.json](../../parameters/security-json.md)のパラメータAspNetCoreDataProtectionでは、ASP.NET Coreデータ保護キーの保存先を指定できます。データ保護キーは、認証Cookie、CSRFトークン、その他の保護対象データの暗号化に用いるXMLデータです。

指定可能なデータ保護キーの保存先（永続化先）は以下のとおりです。プリザンターのバージョンにより指定可能な保存先が異なります。

| 保存先                           | 対応バージョン |
| :------------------------------- | :------------- |
| Azure（Blob Storage＋Key Vault） | 1.3.21.0以降   |
| データベース（Sessionsテーブル） | 1.3.21.0以降   |
| KVS                              | 1.5.7.0以降    |

※Azure Blob Storageは、データ保護キーの保存先です。  
※Azure Key Vaultは、データ保護キーを保護する暗号化キーの保存先です。

### 1-1. パラメータ一覧

[Security.json](../../parameters/security-json.md)のパラメータAspNetCoreDataProtection以下には、以下のパラメータがあります。各パラメータの設定例は後述します。

- 保存先ごとに指定が必要なパラメータが異なります。  
- 保存先をデータベース（Sessionsテーブル）とし、各パラメータの指定を省略した場合はシステムが自動的に設定する固定文字列が適用されます。

| パラメータ名                  | 説明                                                      | Azure | KVS | DB  |
| ----------------------------- | --------------------------------------------------------- | :---: | :-: | :-: |
| BlobContainerUri              | Azure Blob Storageに保存したデータ保護キーのコンテナURL。 |  ✓   |     |     |
| KeyIdentifier                 | Azure Key Vaultに保存した暗号化キーのURL。                |  ✓   |     |     |
| KeyFileName                   | Azure Blob Storageに保存したデータ保護キーのファイル名。  |  ✓   |     |     |
| XmlAesKey                     | データ保護キーをAESで暗号化するための鍵素材。             |     | ✓  | （✓） |
| KeyValueStoreConnectionString | KVS接続文字列。                                           |       | ✓  |     |
| KeyValueStoreKeyName          | KVSに保存したデータ保護キーの名前。                     |       | ✓  |     |

### 1-2. データ保護キーの保存先の決定方法（優先順位）

データ保護キーの保存先は、プリザンター起動時に、以下の優先順位に基づき決定されます。保存先をAzureとする指定がある場合は、KVSとする指定があったとしても、Azureとする指定が優先されます。

| 優先<br>順位 | 条件                                                          | 保存先                           |
| -------: | :------------------------------------------------------------ | :------------------------------- |
|        1 | BlobContainerUriとKeyIdentifierが設定されている         | Azure Blob Storage＋Key Vault    |
|        2 | 上記が未設定<br>かつKeyValueStoreConnectionStringが設定されている | KVS                              |
|        3 | 上記がいずれも未設定                                          | データベース（Sessionsテーブル） |

### 1-3. データ保護キーの暗号化

保存先としてAzureまたはKVSを指定する場合、データ保護キーを外部に保存することになるため、AESで暗号化します。AES暗号化時には、[Security.json](../../parameters/security-json.md)のパラメータXmlAesKeyをAES鍵素材として使用します。そのため保存先としてAzureまたはKVSを指定する場合は、XmlAesKeyの設定が必須です。

なお、保存先としてデータベース（Sessionsテーブル）を使用する場合では、サービス名（[Service.json](../../parameters/service-json.md)のパラメータNameの値）が既定のAES鍵素材として使用されます（XmlAesKeyがnullの場合）。

### 1-4. データ保護キーのファイル名

データ保護キーのファイル名は、以下の各パラメータで指定します。

| 保存先             | パラメータ           | 設定例                                |
| :----------------- | :------------------- | :------------------------------------ |
| Azure Blob Storage | KeyFileName          | "keys.xml"                            |
| KVS                | KeyValueStoreKeyName | "Pleasanter-Prod:DataProtection-Keys" |

KeyValueStoreKeyNameの指定を省略した場合、以下のルールに基づきファイル名が暗黙的に付与されます。

```text
{サービス名}:DataProtection-Keys
```

たとえばサービス名がImplem.Pleasanterの場合、既定のファイル名はImplem.Pleasanter:DataProtection-Keysとなります。1つのKVSを複数環境で共有する場合は、環境ごとにKeyValueStoreKeyNameを分けることでキーリングの衝突を防げます。

### 1-5. ASP.NET Coreデータ保護について

ASP.NET Coreデータ保護の詳細は、以下のマイクロソフト社のドキュメントを確認してください。

1. [ASP.NET Core データ保護の構成](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/configuration/overview)
1. [ASP.NET Core でのデータ保護のキー管理と有効期間](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/configuration/default-settings)
1. [ASP.NET Core でのキー ストレージ プロバイダー](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/implementation/key-storage-providers)

## 2. 前提条件

データ保護キーをKVSで保存する場合の前提条件は、以下のとおりです。

1. データ保護キーをKVSへ保存する場合は、KVSの永続化（AOFまたはRDB）を有効化してください。永続化が無効な状態でKVSを再起動すると、データ保護キーが失われます。データ保護キーが失われた場合、既存の認証Cookie、CSRFトークン、保護済みデータを復号できず、ユーザは再ログインが必要になるなどの影響が発生します。
1. データ保護キーが誤って平文でKVSへ保存されてしまうことを防ぐため、[Security.json](../../parameters/security-json.md)のパラメータXmlAesKeyを必ず指定してください。XmlAesKeyを指定せずにKVSへの保存を有効化した場合、プリザンターはエラーとなり起動しません。
1. 複数インスタンスでデータ保護キーを共有する場合、複数インスタンス間で「Security.json」のパラメータKeyValueStoreConnectionStringとXmlAesKey、およびサービス名（アプリケーション名）が同一である必要があります。
1. 1つのKVSを複数環境で共有する場合は、「Security.json」のパラメータKeyValueStoreKeyNameを環境ごとに分けて、データ保護キーの衝突を防いでください。

## 3. 設定例（パラメータファイルによる設定）

### 3-1. データ保護キーの保存先としてAzureを指定する場合

##### Security.json

```json
    "AspNetCoreDataProtection": {
        "BlobContainerUri": "https://stragename.blob.core.windows.net/containername",
        "KeyIdentifier": "https://keyvalult-name.vault.azure.net/keys/key-name/...",
        "KeyFileName": "Keys.xml",
        "XmlAesKey":null,
        "KeyValueStoreConnectionString":null,
        "KeyValueStoreKeyName": null
    },
```

| パラメータ                        | 注意事項                                                                                                                     |
| :-------------------------------- | :--------------------------------------------------------------------------------------------------------------------------- |
| BlobContainerUri<br>KeyIdentifier | 保存先としてAzureを指定する場合、これらのパラメータの指定が必須です。                                                        |

### 3-2. データ保護キーの保存先としてKVSを指定する場合

##### Security.json

```json
    "AspNetCoreDataProtection": {
        "BlobContainerUri": null,
        "KeyIdentifier": null,
        "KeyFileName": null,
        "XmlAesKey": "a0b1c2...",
        "KeyValueStoreConnectionString": "localhost:6379,abortConnect=false",
        "KeyValueStoreKeyName": "Pleasanter:DataProtection-Keys"
    },
```

| パラメータ                    | 注意事項                                                                                                                                                                                                                                                                                                                                                                                                 |
| :---------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| XmlAesKey                     | クラスタ環境の場合はすべてのプリザンターで同じ文字列を指定してください。                                                                                                                                                                                                                                                                                                                                 |
| KeyValueStoreConnectionString | 接続文字列の末尾にabortConnect=falseを必ず付与してください。KVSへ接続できない場合、プリザンターが起動に失敗する可能性があります（たとえばStackExchange.Redisの既定はabortConnect=trueとなっています）。abortConnect=falseを付与した場合、起動時にKVSが一時的に不通でも起動を継続し、接続はバックグラウンドで再試行されます。<br>クラスタ環境の場合はすべてのプリザンターで同じ文字列を指定してください。 |

クラスタ環境の場合は、上記注意事項に加えて、サービス名に同じ文字列を指定する必要があります。

### 3-3. 複数の環境で1つのKVSを共有する場合

環境ごとにKeyValueStoreKeyNameを変えて、キーリングの衝突を防ぎます。

##### Security.json（本番環境）

```json
    "AspNetCoreDataProtection": {
            ：省略
        "KeyValueStoreConnectionString": "redis.example.com:6379,abortConnect=false",
        "KeyValueStoreKeyName": "Pleasanter-Prod:DataProtection-Keys"
    },
```

##### Security.json（検証環境）

```json
    "AspNetCoreDataProtection": {
            ：省略
        "KeyValueStoreConnectionString": "redis.example.com:6379,abortConnect=false",
        "KeyValueStoreKeyName": "Pleasanter-Stg:DataProtection-Keys"
    },
```

### 3-4. データ保護キーの保存先としてデータベース（Sessionsテーブル）を指定する場合

データ保護キーの保存先としてデータベース（Sessionsテーブル）を指定する場合、[Security.json](../../parameters/security-json.md)を編集する必要はありません。

##### Security.json（既定の設定）

```json
    "AspNetCoreDataProtection": {
        "BlobContainerUri": null,
        "KeyIdentifier": null,
        "KeyFileName": "Keys.xml",
        "XmlAesKey": null,
        "KeyValueStoreConnectionString": null,
        "KeyValueStoreKeyName": null
    },
```

## 4. システム環境変数への登録方法

以下の各パラメータの値は、システム環境変数に登録できます。

1. BlobContainerUri
1. KeyIdentifier
1. XmlAesKey
1. KeyValueStoreConnectionString
1. KeyValueStoreKeyName

システム環境変数への登録については以下のページも確認してください。  
「パラメータ設定：資格情報をシステム環境変数に登録する」

### 4-1. 命名規則

システム環境変数の命名規則は以下の通りです。

```text
（サービス名）_Security_AspNetCoreDataProtection_BlobContainerUri
（サービス名）_Security_AspNetCoreDataProtection_KeyIdentifier
（サービス名）_Security_AspNetCoreDataProtection_XmlAesKey
（サービス名）_Security_AspNetCoreDataProtection_KeyValueStoreConnectionString
（サービス名）_Security_AspNetCoreDataProtection_KeyValueStoreKeyName
```

|項目	|必須	|説明|
|:--|:--|:--|
|サービス名	|○	|[Service.json](../../parameters/service-json.md)のEnvironmentNameまたはNameの値を指定|

#### 4-1-1. 設定例

|変数	|設定例|
|:--|:--|
|Implem.Pleasanter_Security_AspNetCoreDataProtection_BlobContainerUri|	https\://stragename.blob.core.windows.net/containername|
|Implem.Pleasanter_Security_AspNetCoreDataProtection_KeyIdentifier|	https\://keyvalult-name.vault.azure.net/keys/key-name/....|
|Implem.Pleasanter_Security_AspNetCoreDataProtection_XmlAesKey|	a0b1c2...|
|Implem.Pleasanter_Security_AspNetCoreDataProtection_KeyValueStoreConnectionString|redis.example.com:6379,abortConnect=false|
|Implem.Pleasanter_Security_AspNetCoreDataProtection_KeyValueStoreKeyName|Pleasanter-Stg:DataProtection-Keys|

### 4-2. 優先順

本パラメータファイルとシステム環境の両方に設定した場合や省略形で設定した場合の優先順位は以下のとおりです。

#### 4-2-1. BlobContainerUriの優先順

|優先順|設定値|
|:--|:--|
|1	|本パラメータファイルの「BlobContainerUri」|
|2	|環境変数の「（サービス名：EnvironmentName）_Security_AspNetCoreDataProtection_BlobContainerUri」|
|3	|環境変数の「（サービス名：Name）_Security_AspNetCoreDataProtection_BlobContainerUri」|

#### 4-2-2. KeyIdentifierの優先順

|優先順	|設定値|
|:--|:--|
|1	|本パラメータファイルの「KeyIdentifier」|
|2	|環境変数の「（サービス名：EnvironmentName）_Security_AspNetCoreDataProtection_KeyIdentifier」|
|3	|環境変数の「（サービス名：Name）_Security_AspNetCoreDataProtection_KeyIdentifier」|

#### 4-2-3. XmlAesKeyの優先順

|優先順	|設定値|
|:--|:--|
|1	|本パラメータファイルの「KeyIdentifier」|
|2	|環境変数の「（サービス名：EnvironmentName）_Security_AspNetCoreDataProtection_XmlAesKey」|
|3	|環境変数の「（サービス名：Name）_Security_AspNetCoreDataProtection_XmlAesKey」|

#### 4-2-4. KeyValueStoreConnectionStringの優先順

|優先順	|設定値|
|:--|:--|
|1	|本パラメータファイルの「KeyIdentifier」|
|2	|環境変数の「（サービス名：EnvironmentName）_Security_AspNetCoreDataProtection_KeyValueStoreConnectionString」|
|3	|環境変数の「（サービス名：Name）_Security_AspNetCoreDataProtection_KeyValueStoreConnectionString」|

#### 4-2-5. KeyValueStoreKeyNameの優先順

|優先順	|設定値|
|:--|:--|
|1	|本パラメータファイルの「KeyIdentifier」|
|2	|環境変数の「（サービス名：EnvironmentName）_Security_AspNetCoreDataProtection_KeyValueStoreKeyName」|
|3	|環境変数の「（サービス名：Name）_Security_AspNetCoreDataProtection_KeyValueStoreKeyName」|

### 4-3. システム環境変数に登録する際の注意点

「2. 優先順」に記載の通りパラメータファイルに設定した値が最優先となるため、システム環境変数に登録する場合はパラメータファイルでは「null」を指定してください。

## 5. 対応バージョン

| 対応バージョン | 内容                                                                                |
| -------------- | ----------------------------------------------------------------------------------- |
| 1.3.21.0以降   | 機能追加                                                                            |
| 1.5.7.0以降    | 以下のパラメータを追加<br>・KeyValueStoreConnectionString<br>・KeyValueStoreKeyName |

## 6. 関連情報

-   [ASP.NET Core データ保護の構成](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/configuration/overview)
-   [ASP.NET Core でのデータ保護のキー管理と有効期間](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/configuration/default-settings)
-   [ASP.NET Core でのキー ストレージ プロバイダー](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/implementation/key-storage-providers)
