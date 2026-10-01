---
title: Scim.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: scim-json
translationKey: scim-json
shortname: Scim.json
created: 2026-08-13
updated: 2026-09-08
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/parameters/assets/1bb0195dff4743a6bbb5a8f3aa44e8e1.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/parameters/assets/038a7114735c417494bbd08b3e552353.svg#only-dark)](https://pleasanter.org/support/)

## 注意事項

1. パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)をご確認ください。

## 設定値

本パラメータファイルの設定値は以下の通りです。

| パラメータ名       | 設定例   | 説明                                                                                                                                                                                                                           |
| ------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Enabled            | true     | 「SCIM」によるユーザ情報およびグループ情報の連携を有効にするかどうかを指定します。<br>本パラメータの設定はプリザンター全体に影響します。<br>テナントごとの連携可否は、テナント管理画面で発行するSCIMトークンで管理してください。 |
| SwaggerEnabled     | false    | SCIM機能の動作確認や、アプリ開発時の確認に使う画面を表示するかどうかを指定します。<br>一般ユーザが日常的に使う画面ではありません。<br>本番環境では、必要がない場合、falseに設定してください。                                  |
| ExtendedAttributes | 下記参照 | SCIMの属性を、ユーザ管理画面またはグループ管理画面に追加した「拡張項目」に保存するための設定です。<br>詳細は以下の「ExtendedAttributes」を参照してください。                                                                   |

## 設定例

```json
{
    "Enabled": true,
    "SwaggerEnabled": false,
    "ExtendedAttributes": {
        "Users": [
            {
                "Schema": "urn:pleasanter:params:scim:schemas:extension:custom:2.0:User",
                "Name": "jobTitle",
                "ColumnName": "Users_ClassB"
            }
        ],
        "Groups": [
            {
                "Schema": "urn:pleasanter:params:scim:schemas:extension:custom:2.0:Group",
                "Name": "groupType",
                "ColumnName": "Groups_ClassA"
            }
        ]
    }
}
```

## ExtendedAttributes

ExtendedAttributesは、IDプロバイダ側の「属性」を、プリザンターの「ユーザ管理」画面または「グループ管理」画面に追加した「拡張項目」に紐づけるための設定です。

たとえば、IDプロバイダ側の属性「役職（jobTitle）」を、ユーザ管理画面の「拡張項目」「Users_ClassB」に保存したい場合は、以下のように設定します。

```json
"ExtendedAttributes": {
    "Users": [
        {
            "Schema": "urn:pleasanter:params:scim:schemas:extension:custom:2.0:User",
            "Name": "jobTitle",
            "ColumnName": "Users_ClassB"
        }
    ],
    "Groups": []
}
```

### ExtendedAttributes.Users

ユーザに対する拡張属性のマッピングを設定します。

例:

```json
"Users": [
    : 中略
]

"Groups": [
    {
        "Schema": "urn:pleasanter:params:scim:schemas:extension:custom:2.0:Group",
        "Name": "groupType",
        "ColumnName": "Groups_ClassA"
    },
    {
        "Schema": "urn:pleasanter:params:scim:schemas:extension:custom:2.0:Group",
        "Name": "groupNote",
        "ColumnName": "Groups_DescriptionA"
    }
]
```

この例では、次のように保存されます。

| SCIM属性       | プリザンター保存先 |
| :------------- | :----------------- |
| jobTitle       | Users_ClassB       |
| officeLocation | Users_DescriptionA |

Entra ID側の属性マッピングでは、次のようにスキーマを含めた完全な属性名を指定します。

| プリザンター保存先 | Entra ID側で指定するSCIM属性                                                |
| :----------------- | :-------------------------------------------------------------------------- |
| Users_ClassB       | urn:pleasanter:params:scim:schemas:extension:custom:2.0:User:jobTitle       |
| Users_DescriptionA | urn:pleasanter:params:scim:schemas:extension:custom:2.0:User:officeLocation |

### ExtendedAttributes.Groups

グループに対する拡張属性のマッピングを設定します。

例:

```json
"Groups": [
    {
        "Schema": "urn:pleasanter:params:scim:schemas:extension:custom:2.0:Group",
        "Name": "groupType",
        "ColumnName": "Groups_ClassA"
    },
    {
        "Schema": "urn:pleasanter:params:scim:schemas:extension:custom:2.0:Group",
        "Name": "groupNote",
        "ColumnName": "Groups_DescriptionA"
    }
]
```

この例では、以下のように保存されます。

| SCIM属性  | プリザンター保存先  |
| :-------- | :------------------ |
| groupType | Groups_ClassA       |
| groupNote | Groups_DescriptionA |

Entra ID側の属性マッピングでは、以下のようにスキーマを含めた完全な属性名を指定します。

| プリザンター保存先  | Entra ID側で指定するSCIM属性                                            |
| :------------------ | :---------------------------------------------------------------------- |
| Groups_ClassA       | urn:pleasanter:params:scim:schemas:extension:custom:2.0:Group:groupType |
| Groups_DescriptionA | urn:pleasanter:params:scim:schemas:extension:custom:2.0:Group:groupNote |

ExtendedAttributes.UsersとExtendedAttributes.Groupsでは、以下のパラメータを設定します。

| 項目       | 内容                           |
| :--------- | :----------------------------- |
| Schema     | SCIMの拡張スキーマ             |
| Name       | SCIM側の属性名                 |
| ColumnName | プリザンター側の保存先カラム名 |

#### Schema

SCIMの拡張スキーマを設定します。

1. プリザンター側のスキーマ設定は省略可能です。
1. IDプロバイダ側の属性マッピングでは、完全な属性名を設定する必要があります。

|   拡張項目の種別 | SCIMの拡張スキーマ                                            |
| ---------------: | :------------------------------------------------------------ |
|   ユーザ拡張項目 | urn:pleasanter:params:scim:schemas:extension:custom:2.0:User  |
| グループ拡張項目 | urn:pleasanter:params:scim:schemas:extension:custom:2.0:Group |

#### Name

IDプロバイダ側の「属性マッピング」で使う属性名の末尾文字列を指定します。

##### IDプロバイダ側のSCIM属性名

```text
urn:pleasanter:params:scim:schemas:extension:custom:2.0:User:jobTitle
```

##### Scim.jsonのNameの設定例

```json
"Name": "jobTitle"
```

#### ColumnName

プリザンター側で保存先とする「拡張項目」のカラム名を指定します。

1. 「ユーザ管理」画面に追加した「拡張項目」に保存する場合は、接頭辞Users_を添えた「拡張項目」のカラム名を指定します。
1. 「グループ管理」画面に追加した「拡張項目」に保存する場合は、接頭辞Groups_を添えた「拡張項目」のカラム名を指定します。

例:

```json
"ColumnName": "Users_ClassB"
```

### 指定できるプリザンター側の項目

SCIMの拡張属性の保存先として利用できるのは、「ユーザ管理」画面または「グループ管理」画面の「拡張項目」です。

主に次の列を指定します。

```text
Users_ClassA
Users_ClassB
Users_ClassC
Users_DescriptionA
Users_DescriptionB

Groups_ClassA
Groups_ClassB
Groups_ClassC
Groups_DescriptionA
Groups_DescriptionB
```

Class系とDescription系の拡張項目を利用できます。

実際に画面上で表示する場合は、別途CustomDefinitions\Column.jsonで表示名などを設定します。

### 拡張項目の表示名を設定する場合

プリザンターの画面上で拡張項目を表示したい場合は、CustomDefinitions\Column.jsonを設定します。

対象フォルダ:

```text
Implem.PURIZANNTA- \App_Data\Parameters\CustomDefinitions
```

ファイル名:

```text
Column.json
```

設定例:

```json
{
    "Users_ClassB": {
        "LabelText": "役職",
        "GridEnabled": "1",
        "EditorEnabled": "1"
    },
    "Groups_ClassA": {
        "LabelText": "グループ種別",
        "GridEnabled": "1",
        "EditorEnabled": "1"
    }
}
```

この例では、次のように表示されます。

| 列名          | 画面上の表示名 |
| :------------ | :------------- |
| Users_ClassB  | 役職           |
| Groups_ClassA | グループ種別   |

### Microsoft Entra ID側で指定する属性名

Microsoft Entra IDの属性マッピングでは、プリザンター側のNameだけではなく、スキーマを含めた完全な属性名を指定します。

例として、Scim.jsonに次の設定をした場合:

```json
{
    "Schema": "urn:pleasanter:params:scim:schemas:extension:custom:2.0:User",
    "Name": "jobTitle",
    "ColumnName": "Users_ClassB"
}
```

Entra ID側では、customappsso属性に次の値を指定します。

```text
urn:pleasanter:params:scim:schemas:extension:custom:2.0:User:jobTitle
```

jobTitleだけを指定しても、期待した形で連携されない可能性があります。
Entra ID側では、必ず完全な属性名を指定してください。

## 対応バージョン

| 対応バージョン | 内容            |
| -------------- | --------------- |
| 1.5.8.0 以降   | Scim.jsonを追加 |

## 関連情報

-   [パラメータ変更時の確認事項](parameter-edit.md)
