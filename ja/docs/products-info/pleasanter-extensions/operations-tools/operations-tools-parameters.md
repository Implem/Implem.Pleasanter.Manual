---
title: パラメータ一覧
category: 運用支援ツール
order: '16000'
status: ''
parts: ''
urlstring: operations-tools-parameters
translationKey: operations-tools-parameters
shortname: Pleasanter Extensions,Operations Tools,パラメータ一覧
created: 2025-01-27
updated: 2025-02-14
---

## 概要

プリザンターのパラメータ一覧と設定値の変更有無を確認できる画面です。プリザンターのパラメータファイルはJSON形式ですが、表形式として参照することやCSVファイルにエクスポート出力することが可能です。また、「ファイル名」「パラメータ名」を指定してフィルタすることができます。明細情報は「ファイル名」の昇順、各ファイルの上から順で表示されます。  

![パラメータ一覧画面。プリザンターのパラメータを表形式で表示する](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/11d6c79b312347a6a7051c80e47e7cfa.png)

| 表示種別 | 項目 | 説明                                      |
|------|----|-----------------------------------------|
| 表形式  | ファイル名 | パラメータのファイル名の情報が表示されます。 |
| 表形式  | パラメータ名 | パラメータ名の情報が表示されます。 |
| 表形式  | パラメータ値：変更前（既定値） | Operations Toolsの「DefaultParametersDir」に配置されたファイルの設定値が表示されます。 |
| 表形式  | パラメータ値：変更後 | プリザンターのパラメータファイルの設定値が表示されます。 |
| 表形式  | 変更有無 | パラメータ値の「変更前（既定値）」と「変更後」で値が異なる場合は、赤背景で「あり」と表示されます。 |

また、セキュリティの観点から次の表に示した一部のパラメータでは、パラメータ値を「*」とマスキングした状態で表示します。

| ファイル名          | パラメータ名                                                     | 
| ------------------- | ---------------------------------------------------------------- | 
| Authentication.json | LdapParameters[0].LdapSyncPassword                               | 
| Authentication.json | SamlParameters.IdentityProviders[0].SigningCertificate.FindValue | 
| Kvs.json            | ConnectionStringForSession                                       | 
| Mail.json           | SmtpPassword                                                     | 
| Migration.json      | SourceConnectionString                                           | 
| Rds.json            | SaConnectionString                                               | 
| Rds.json            | OwnerConnectionString                                            | 
| Rds.json            | UserConnectionString                                             | 
| Security.json       | AllowIpAddresses                                                 | 
| Security.json       | XmlAesKey                                                        | 
| Security.json       | BlobContainerUri                                                 | 
| Security.json       | KeyIdentifier                                                    | 
| Security.json       | KeyFileName                                                      | 
| Service.json        | DefaultPassword                                                  | 

> **Note**  
> ご利用中のプリザンターのバージョンにおける変更前のパラメータJSONファイルをDefaultParametersフォルダ配下に配置することで、差分を比較することができます。  
> 
> 配置場所の例：  
> C:\web\pleasanter\Implem.Pleasanter\ExtendedLibraries\OperationsTools\App_Data\DefaultParameters  
> 
> 変更前のパラメータJSONファイルがお手元にない場合は、GitHubのリリース用ページからダウンロードして取得してください。  
> https://github.com/Implem/Implem.Pleasanter/releases  

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.1 以降|セキュリティの観点から一部のパラメータ値を「*」とマスキングした状態で表示するように修正|
