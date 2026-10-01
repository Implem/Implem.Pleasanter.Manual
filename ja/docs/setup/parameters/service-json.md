---
title: Service.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: service-json
translationKey: service-json
shortname: Service.json
created: 2019-04-30
updated: 2026-06-09
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Name|"Implem.Pleasanter"|Pleasanterのサービスの名称を指定。この名称と同じ名前のデータベースに接続。|
|EnvironmentName|"Implem.Pleasanter.Env"|Pleasanterの資格情報をシステム環境変数から取得する際に用いる環境名を指定。|
|TimeZoneDefault|"Tokyo Standard Time"|CodeDefinerの実行時に参照。Pleasanterの既定のタイムゾーンを指定。※1※3<br>ver1.4.6以降ではCodeDefiner実行時に引数で指定した内容で設定する。|
|DefaultPassword|"pleasanter"|インストール時に作成されるAdministratorの初期パスワードを指定。|
|DeploymentEnvironment|"production"|プリザンターがインストールされている環境（本番環境、ステージング環境など）を区別するための文字列を指定。[BackgroundService.json](background-service-json.md)の EnvironmentVariables で使用。システム環境変数に登録可能。※2|
|WithoutChangeDefaultPassword|false|インストール時に作成されるAdministratorの初期パスワードの変更を不要とする場合はtrueを指定。|
|DefaultLanguage|"ja"|Pleasanterの既定の言語を指定。※3<br>ver1.4.6以降ではCodeDefiner実行時に引数で指定した内容で設定する。|
|AbsoluteUri|"http://pleasanter.example.local"|通知やリマインダーに記載されるURLの先頭部分を指定。nullに指定した場合には現在接続中のURLが使用される。 **URI文字列の末尾には / (スラッシュ)は不要**|
|MaxRequestBodySize|30000000|CSVのインポート時またはAPIで添付ファイルをPOSTする場合に既定値の3000万バイト（約 28.6 MB）を超えるサイズで送りたい場合に指定。|
|RequireHttps|false|httpsによる接続を強制する場合はtrue、それ以外はfalseを指定。|
|AnnouncementSiteId|1234|サービスのアナウンスを表示するサイトIDを指定。|
|ShowProfiles|true|[ユーザの管理](../../managers-guide/user-administration/index.md)画面および[プロファイル編集](../../users-guide/common/profile.md)画面の有効化/無効化をtrue/falseで指定。|
|ShowChangePassword|false|ナビゲーションメニューにパスワード変更を表示する設定をtrue/falseで指定。|
|ShowStartGuide|true|スタートガイドの有効化/無効化をtrue/falseで指定。|
|Demo|true|デモ環境の有効化/無効化をtrue/falseで指定。|
|DemoUsagePeriod|60|デモ環境の利用期限を計算するための日数を指定。|

※1 PleasanterをインストールするサーバのOSで有効なタイムゾーンを設定してください。（Windowsなら"Tokyo Standard Time"など、Linuxなら"Asia/Tokyo"など）
※2 DeploymentEnvironment の値は通常、環境変数に設定して使います。
※3 言語、タイムゾーンは以下マニュアルページを参照ください。
[FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../FAQ/system-requirements-and-setup/faq-supported-language.md)

## システム環境変数への登録方法

DeploymentEnvironmentは[システム環境変数に登録](credentials-in-environment-variables.md)できます。システム環境変数への登録については以下ページも参照ください。  
[パラメータ設定：資格情報をシステム環境変数に登録する](credentials-in-environment-variables.md)

### 1. 命名規則

システム環境変数の命名規則は以下の通りです。
```
（サービス名）_Service_DeploymentEnvironment
```

|項目|必須|説明|
|---|---|---|
|サービス名|○|「Service.json」の「EnvironmentName」または「Name」を指定|

#### 設定例

|変数|値|
|:--|:--|
|Implem.Pleasanter_Service_DeploymentEnvironment|production|

### 2. 優先順

本パラメータファイルとシステム環境の両方に設定した場合や省略形で設定した場合の優先順位は以下のとおりです。

#### 1. DeploymentEnvironmentの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「DeploymentEnvironment」|
|2|環境変数の「（サービス名：EnvironmentName）_Service_DeploymentEnvironment」|
|3|環境変数の「（サービス名：Name）_Service_DeploymentEnvironment」|

### 3. システム環境変数に登録する際の注意点

「2. 優先順」に記載の通りパラメータファイルに設定した値が最優先となるため、システム環境変数に登録する場合はパラメータファイルでは「null」を指定してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.6.0 以降|WithoutChangeDefaultPasswordの追加|
|1.3.7.0 以降|MaxRequestBodySizeの追加|
|1.3.26.0 以降|AnnouncementSiteIdの追加<br>DeploymentEnvironmentの追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [パラメータ設定：BackgroundService.json](background-service-json.md)
-   [ユーザ管理機能](../../managers-guide/user-administration/index.md)
-   [共通機能：プロファイル編集](../../users-guide/common/profile.md)
-   [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../FAQ/system-requirements-and-setup/faq-supported-language.md)
-   [パラメータ設定：資格情報をシステム環境変数に登録する](credentials-in-environment-variables.md)
