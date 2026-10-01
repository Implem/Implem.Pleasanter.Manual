---
title: カスタム属性の連携設定
category: 追加設定：アカウント連携
order: '400'
status: ''
parts: ''
urlstring: scim-sync-custom-attributes
translationKey: scim-sync-custom-attributes
shortname: カスタム属性の連携設定
created: 2026-08-13
updated: 2026-09-08
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/6461453c544b4368b1351071c396c953.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/944dcfcdcc204213a19205a5e0589d0a.svg#only-dark)](https://pleasanter.org/support/)

## 概要

IDプロバイダ側に固有の情報（たとえば、役職など）を、「[SCIM機能](index.md)」を用いてプリザンターの拡張項目へ保存したい場合は、IDプロバイダの設定にカスタム属性マッピングを追加する必要があります。以下では、Microsoft Entra IDの「jobTitle」（役職）をプリザンターの「[拡張項目](../../../../developers-guide/extended-features/extended-column.md)」「Users_ClassB」へ連携する手順を例に説明します。

## 前提条件

1.  [年間サポートサービス](https://pleasanter.org/support/)の下記プラン契約者限定の機能です。

    | エントリー | ベーシック | ベーシックプラス | ビジネス | ビジネスプラス | アンリミテッド |
    | :--------: | :--------: | :--------------: | :------: | :------------: | :------------: |
    |            |            |        〇        |    〇    |       〇       |       〇       |

1.  「[分類](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)」Bを「[拡張項目](../../../../developers-guide/extended-features/extended-column.md)」として追加してください。

## 操作手順

### プリザンター側の設定

プリザンター側では、[Scim.json](../../../parameters/scim-json.md)のパラメータ「ExtendedAttributes」に、完全なSCIM属性名とプリザンターでの保存先となる「[拡張項目](../../../../developers-guide/extended-features/extended-column.md)」のカラム名を設定します。

``` json title="Scim.jsonの設定例" linenums="1" hl_lines="4-13"
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
        "Groups": []
    }
}
```

「Schema」と「Name」には、IDプロバイダ側で追加する完全なSCIM属性名を、以下のように分割して設定します。

![IDプロバイダ側で追加する完全なSCIM属性名](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/e5477ae353d04153ba365f19749716f0.png)

| 設定項目   | 値                                                           |
| :--------- | :----------------------------------------------------------- |
| Schema     | urn:pleasanter:params:scim:schemas:extension:custom:2.0:User |
| Name       | jobTitle                                                     |
| ColumnName | Users_ClassB                                                 |

### IDプロバイダ側の設定

#### カスタム属性を追加する

Microsoft Entra ID側では、customappssoの属性リストにカスタム属性を追加します。

1.  「Microsoft Entra 管理センター」を開いてください。
1.  対象の「エンタープライズ アプリケーション」を開いてください。
1.  画面左側のメニューから「プロビジョニング」を開いてください。
1.  「マッピング」を開いてください。
1.  「Provision Microsoft Entra ID Users」を選択してください。
1.  画面下部の「詳細オプションの表示」をクリックしてオンにしてください。
1.  「customappsso の属性リストを編集します」をクリックしてください。

    ![「customappsso の属性リストを編集します」をクリック](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/bad3c6b9f91843c7b4c870053590487c.png)

1.  属性リストの編集画面で、次の属性を追加します。

    | 項目   | 設定値                                                                |
    | :----- | :-------------------------------------------------------------------- |
    | 名前   | urn:pleasanter:params:scim:schemas:extension:custom:2.0:User:jobTitle |
    | 型     | String                                                                |
    | 主キー | いいえ                                                                |
    | 必須   | いいえ                                                                |

    ![属性リストの編集画面で追加すべき属性](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/9899bee963ab4fe3b3e3562011e7b73a.png)

1.  追加後、属性リストを保存してください。

### 追加したカスタム属性へマッピングする

Microsoft Entra IDの属性を、追加したカスタム属性へマッピングします。

1.  「Provision Microsoft Entra ID Users」の属性マッピング画面を開いてください。
2.  「新しいマッピングの追加」を選択してください。
3.  以下のように設定してください。

    | 項目                     | 設定値                                                                |
    | :----------------------- | :-------------------------------------------------------------------- |
    | マッピングの種類         | 直接                                                                  |
    | ソース属性               | jobTitle                                                              |
    | ターゲット属性           | urn:pleasanter:params:scim:schemas:extension:custom:2.0:User:jobTitle |
    | このマッピングを適用する | 常時                                                                  |

    ![属性マッピング画面での設定](https://pleasanter.org/files/images/ja/setup/additional/account-integration/scim/assets/49d98807f3a44f7087a6d4fa32e8b7ca.png)

1.  設定が済んだら、保存してください。
1.  属性マッピング画面全体も保存が必要です。

### 既定のマッピング設定を変更する

#### Microsoft Entra ID側の設定

Microsoft Entra IDの既定のマッピングに「jobTitle」などの属性が存在する場合は、新しいマッピングを追加する代わりに、既存の「ターゲット属性」を変更しても構いません。

##### プリザンターが使用しない「title」へのマッピングを、プリザンター用のカスタム属性へ置き換え

| ソース属性 | 変更前のターゲット属性 | 変更後のターゲット属性                                                |
| :--------- | :--------------------- | :-------------------------------------------------------------------- |
| jobTitle   | title                  | urn:pleasanter:params:scim:schemas:extension:custom:2.0:User:jobTitle |

jobTitleだけをターゲット属性に指定しても、連携されません。Microsoft Entra ID側では、拡張スキーマを含めた完全なSCIM属性名を指定してください。

#### プリザンター側の設定

変更後のターゲット属性と、プリザンター側の[Scim.json](../../../parameters/scim-json.md)の設定は、下表のように対応させてください。

| 項目                   | 値                                                                    |
| :--------------------- | :-------------------------------------------------------------------- |
| 変更後のターゲット属性 | urn:pleasanter:params:scim:schemas:extension:custom:2.0:User:jobTitle |
| Schema                 | urn:pleasanter:params:scim:schemas:extension:custom:2.0:User          |
| Name                   | jobTitle                                                              |
| ColumnName             | Users_ClassB                                                          |

## 対応バージョン

| 対応バージョン | 内容     |
| -------------- | -------- |
| 1.5.8.0 以降   | 機能追加 |

## 関連情報

-   [SCIM機能](index.md)
-   [プリザンターの初期設定](scim-pleasanter-setup.md)
-   [IDプロバイダの初期設定](scim-idp-setup.md)
-   [拡張項目](../../../../developers-guide/extended-features/extended-column.md)
-   [SCIMでユーザ情報が連携されない](../../../../FAQ/system-administration-operations-and-settings/faq-scim-sync-failure.md)
