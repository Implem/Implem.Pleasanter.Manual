---
title: プリザンターのバージョンアップ手順(Linux)
category: バージョンアップ
order: '1300'
status: ''
parts: ''
urlstring: version-up-net-core
translationKey: version-up-net-core
shortname: バージョンアップ手順,Linuxのバージョンアップ手順
created: 2020-05-29
updated: 2026-01-13
---

## 概要

Linux系OSで運用しているプリザンターのバージョンアップ手順は以下の通りとなります。  

## 注意事項

1. 現在運用中のパラメータファイルを最新バージョンに上書きコピーしないでください。最新バージョンで新たに追加したパラメータが失われ、プリザンターが起動しない恐れがあります。
1. Enterprise Editionにアップグレードし項目拡張を実施している場合は、[Enterprise Edition - バージョンアップ手順](../../../products-info/enterprise-edition/version-up/index.md)に従ってバージョンアップを実施してください。
1. Pleasanter Extensionsの[トライアル](../../../developers-guide/index.md)を実施中の場合は、「Pleasanter Extensionsのトライアルの注意点」を確認してください。
1.CodeDefiner実行時に/l、/zのパラメータを設定しないでください。

## 前提条件

1. プリザンターを起動するユーザが登録されていること。手順の中で記載している **<プリザンターを起動するユーザ>** はこのユーザを指します。
1. プリザンター 1.3 以前のバージョンから、プリザンター 1.4 以降へバージョンアップする場合、[.NET8のインストール](../../installation/install-dotnet/index.md)が必要です。
1. 本手順では.NETを /usr/local/bin にインストールする場合として説明します。同一環境に複数バージョンの.NETが必要などの理由で.NETを異なるディレクトリにインストールする場合は、CodeDefinerの実行時やPleasanterサービス用スクリプトの作成でExecStartに指定するディレクトリをインストール先に合わせて変更してください。

## 手順

バージョンアップ手順は以下の通りです。
1. データベースのバックアップ
1. パラメータファイルのバックアップ
1. プリザンターの準備
   1. アプリケーションの準備
   1. パラメータ再設定
   1. 拡張機能の再設定
1. プリザンターの配置
   1. プリザンターの停止
   1. アプリケーションの配置
1. CodeDefinerの実行
1. プリザンターの起動確認

## 1. データベースのバックアップ

データベースをバックアップします。**Enterprise Editionにアップグレードし、項目を拡張している場合は必ずバックアップしてください**
    [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)

## 2. パラメータファイルのバックアップ

1. パラメータファイルをバックアップします。このバックアップは手順3.2.で使用します。パラメータファイルはマニュアル通りにセットアップした場合、/web/pleasanter/Implem.Pleasanter/App_Data/Parameters/配下のjsonファイルとなります。
1. **拡張機能を利用していない場合は本手順は不要です。** 拡張機能で設定したパラメータファイルをバックアップします。このバックアップは手順3.3.で使用します。拡張機能で設定したファイルはマニュアル通りにセットアップした場合、/web/pleasanter/Implem.Pleasanter/App_Data/Parameters/配下にある以下サブディレクトリ内のファイルとなります。

    |サブディレクトリ名|拡張機能名|備考|
    |:---|:---|:---|
    |CustomDefinitions|[拡張項目](../../../developers-guide/extended-features/extended-column.md)|組織、グループ、ユーザに項目を追加した際に生成されるフォルダ|
    |ExtendedFields|[拡張フィールド](../../../developers-guide/extended-features/extended-fields.md)||
    |ExtendedHtmls|[拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)||
    |ExtendedNavigationMenus|[拡張ナビゲーションメニュー](../../../developers-guide/extended-features/extended-navigationmenus.md)||
    |ExtendedScripts|[拡張スクリプト](../../../developers-guide/extended-features/extended-script.md)||
    |ExtendedServerScripts|[拡張サーバスクリプト](../../../developers-guide/extended-features/extended-server-script.md)||
    |ExtendedSqls|[拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)||
    |ExtendedStyles|[拡張スタイル](../../../developers-guide/extended-features/extended-style.md)||

## 3. プリザンターの準備

### 1. アプリケーションの準備

1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。
1. ダウンロードしたzipファイルを解凍します。

### 2. パラメータ再設定

手順3.1.で準備した最新バージョンモジュールのパラメータファイルに対して、現在設定済みの内容を反映します。[WinMerge](https://winmergejp.bitbucket.io/)などのファイル比較・マージツールを利用して最新バージョンモジュールのパラメータファイルと手順2.で取得したバックアップファイルのパラメータファイルを比較しながら最新バージョンモジュールのパラメータファイルを修正します。    
**Service.jsonのTimeZoneDefaultが正しい値か確認してください。TimeZoneDefaultにはPleasanterをインストールするサーバのOSで有効なタイムゾーンを設定してください。（Windowsなら"Tokyo Standard Time"など、Linuxなら"Asia/Tokyo"など）**  
[FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)    

### 3. 拡張機能の再設定

**拡張機能を利用していない場合は本手順は不要です。** 手順3.1で準備した最新バージョンモジュールの拡張機能用パラメータファイルに対して、現在設定済みの内容を反映します。[WinMerge](https://winmergejp.bitbucket.io/)などのファイル比較・マージツールを利用して最新バージョンモジュールの拡張機能用パラメータファイルと手順2.で取得したバックアップファイルの拡張機能用パラメータファイルを比較しながら最新バージョンモジュールの拡張機能用パラメータファイルを修正します。

## 4. プリザンターの配置

### 1. プリザンターの停止

以下コマンドを実行して、プリザンターを停止します。

```
sudo systemctl stop pleasanter
```

### 2. アプリケーションの配置

1. 手順3.2.でパラメータ再設定した最新バージョンモジュールの「pleasanter」フォルダを[WinSCP](https://winscp.net/jp/)などのファイル転送アプリケーションでサーバの"/web"に配置します。
※念の為、既存の/web/pleasanter/を/web/pleasanter_bk/などとリネームしてバックアップしたうえで、新バージョンを配置することを推奨します。  

1. 以下コマンドを実行して、pleasanterディレクトリ配下の所有者をあらかじめ決めたプリザンターを起動するユーザに変更します。

    ```
    sudo chown -R <プリザンターを起動するユーザ> /web/pleasanter
    ```

## 5. CodeDefinerの実行

以下コマンドを実行して、あらかじめ決めたプリザンターを起動するユーザでCodeDefinerを実行します。/l、/zの引数設定は不要です。

```
cd /web/pleasanter/Implem.CodeDefiner
sudo -u <プリザンターを起動するユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds
```

## 6. プリザンターの起動確認

1. 以下コマンドを実行して、プリザンターを起動します。

    ```
    sudo systemctl start pleasanter
    ```

2. ブラウザでプリザンターのログイン画面を開き、ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。
    ![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/0d80470fa83c40bd99c057d2447549e0.png)
