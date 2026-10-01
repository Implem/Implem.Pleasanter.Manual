---
title: Kvs.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: kvs-json
translationKey: kvs-json
shortname: Kvs.json
created: 2024-10-21
updated: 2025-05-13
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。

|パラメータ名|設定例|説明|
|:--|:--|:--|
|ConnectionStringForSession|<キャッシュのホスト名>:<キャッシュのポート番号>,password=<キャッシュのパスワード>,ssl=True,abortConnect=False|セッションデータに接続するためのセッションの接続文字列を指定。システム環境変数に登録可能。|

## システム環境変数への登録方法

ConnectionStringForSessionは[システム環境変数に登録](credentials-in-environment-variables.md)できます。システム環境変数への登録については以下ページも参照ください。  
[パラメータ設定：資格情報をシステム環境変数に登録する](credentials-in-environment-variables.md)

### 1. 命名規則

システム環境変数の命名規則は以下の通りです。
```
（サービス名）_Kvs_ConnectionStringForSession
```

|項目|必須|説明|
|---|---|---|
|サービス名|○|[Service.json](service-json.md)の「EnvironmentName」または「Name」を指定|

#### 設定例

|変数|値|
|:--|:--|
|Implem.Pleasanter_Kvs_ConnectionStringForSession|<キャッシュのホスト名>:<キャッシュのポート番号>,password=<キャッシュのパスワード>,ssl=True,abortConnect=False|

### 2. 優先順

本パラメータファイルとシステム環境の両方に設定した場合や省略形で設定した場合の優先順位は以下のとおりです。

#### 1. ConnectionStringForSessionの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「ConnectionStringForSession」|
|2|環境変数の「（サービス名：EnvironmentName）_Kvs_ConnectionStringForSession」|
|3|環境変数の「（サービス名：Name）_Kvs_ConnectionStringForSession」|

### 3. システム環境変数に登録する際の注意点

「2. 優先順」に記載の通りパラメータファイルに設定した値が最優先となるため、システム環境変数に登録する場合はパラメータファイルでは「null」を指定してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.10.0 以降|Kvs.jsonを追加|
|1.4.16.0 以降|ConnectionStringForSessionをシステム環境変数に登録する機能を追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [パラメータ設定：資格情報をシステム環境変数に登録する](credentials-in-environment-variables.md)
-   [パラメータ設定：Service.json](service-json.md)
