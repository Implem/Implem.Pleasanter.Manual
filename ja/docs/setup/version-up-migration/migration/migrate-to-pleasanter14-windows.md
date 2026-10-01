---
title: Windows/Windows Serverにインストールしたプリザンター 1.3をプリザンター 1.4へ移行する手順
category: 移行
order: '200'
status: ''
parts: ''
urlstring: migrate-to-pleasanter14-windows
translationKey: migrate-to-pleasanter14-windows
shortname: プリザンター 1.4への移行
created: 2021-07-03
updated: 2026-01-13
---

## 概要

Windows Serverにインストールされているプリザンターをプリザンター 1.4に移行するための手順です。

|対象|移行前|移行後|
|---|---|---|
|OS|Windows/Windows Server|Windows/Windows Server|
|DB|SQL Server|SQL Server|
|Webサーバ|IIS|IIS|
|Platform|.NET 6.0|.NET 8.0|
|Pleasanter|プリザンター 1.3|プリザンター 1.4|

## 注意事項

1. 本手順を実施する前にシステムのバックアップおよびデータベースのバックアップを取得するようにしてください。
1. 移行元の環境の設定ファイル(C:\web\pleasanter\Implem.Pleasanter\App_Data\Parametersフォルダ配下)を編集している場合、移行先の環境へ上書きコピーしないでください。そのまま上書きすると**新しく追加になったパラメータが失われる**可能性がありますので、WinMerge等の差分ツールを使用して、変更部分のみを新しいパラメータファイルにマージしてください。この手順ではWinMergeを使用します。

## 事前確認

Windows/Windows Serverにインストールしているプリザンターのバージョンを確認します。

1. プリザンターへログインします。
1. 画面右上にある「ヘルプ」より「バージョン」をクリックします。
1. バージョンが「1.3.〇.〇」であることを確認します。

## 事前準備

#### 使用ツール

1. WinMergeがインストールされていること。下記ページからダウンロードできます。  
　https://winmergejp.bitbucket.io/  

#### データベースのバックアップ

1. 「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS)マネージャー」を起動してください。

1. 左ペインでサーバ名を選択し、右ペインの「停止」をクリックし、IISを停止してください。
![IISマネージャーの画面。右ペインの「停止」でIISを停止する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/79ffe4e682fc49c9abe8be89508b4e63.png)

1. プリザンターのデータベースのバックアップを取得してください。  
[FAQ：プリザンターのDBデータを定期的にバックアップしたい（SQL Server）](../../../FAQ/backup-restore/faq-backup-schedule.md)

#### モジュールのバックアップ

1. 既存のC:\web\pleasanterをC:\web\pleasanter_bkとリネームしてバックアップしてください。

## .NET8.0のインストール

!!! warning
    .NET8.0の「SDK 8.0.x」と「Hosting Bundle」の2つをインストールしてください。

## 手順

.NETのインストール手順は以下の通りです。

1.  SDKのインストール
1.  Hosting Bundleのインストール

## SDKのインストール

1. ブラウザを起動し、以下のURLへアクセスしてください。  
　https://dotnet.microsoft.com/download/dotnet/8.0

1. 「SDK 8.0.x」をダウンロードし、インストールしてください。
![image](https://pleasanter.org/files/images/ja/setup/installation/install-dotnet/assets/31c43c2944e547c88b8f0620231a12f3.png)

1. コマンドプロンプトまたはPowerShellを起動して以下のコマンドを実行し、「8.0.x」が表示されることを確認してください。
```
 dotnet --version
```

## Hosting Bundleのインストール

1. 「Hosting Bundle」をダウンロードし、インストールしてください。
![image](https://pleasanter.org/files/images/ja/setup/installation/install-dotnet/assets/deba23e6b5474821b6d4ac4e2d0d6b34.png)

## プリザンター 1.4のダウンロード

1. 以下のURLへアクセスしてください。  
　https://pleasanter.org/dlcenter  

1. 「プリザンター 1.4 Community Edition」のダウンロードリンクより、プリザンターをダウンロードしてください。

## モジュールの配置

1. ダウンロードしたプリザンターのモジュールを「C:\web」フォルダに展開してください。

1. WinMergeを起動し、以下の2つのフォルダを比較してください。  
　①C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters  
　②C:\web\pleasanter_bk\Implem.Pleasanter\App_Data\Parameters  

![WinMergeで新旧のParametersフォルダを比較した画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/2c747d29d1ea4e75987f52f5938b1d7c.png)

1. 上記①のParametersフォルダ配下の各パラメータファイルを上記②のParametersフォルダ配下のものと比較しながら修正してください。  
<span class="pl-attention">※「Extended○○」といったフォルダ内部のJSONファイルは、拡張機能を使っていない場合は変更不要です。</span>  

![WinMergeでパラメータファイルの中身を比較しながら修正する画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/589991949bb34f99bb7968937f6a2eb0.png)

パラメータを修正する際、以下のパラメータは移行元のものに合わせて修正する必要がございます。Dbmsは"SQLServer"とし、TimeZoneは"Tokyo Standard Time"に変更してください。

Rds.json

```
"Dbms": "SQLServer"
"TimeZoneInfo": "Tokyo Standard Time"
```

Service.json
```
"TimeZoneDefault": "Tokyo Standard Time"
```

## CodeDefinerの実行

1.コマンドプロンプトを起動し、以下のコマンドを実行してください。
```
cd C:\web\pleasanter\Implem.CodeDefiner
dotnet Implem.CodeDefiner.dll _rds
```

## プリザンターの起動

1. IISマネージャーを起動し、IISを起動してください。
![IISマネージャーの画面。右ペインでIISを起動する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/11e9e5a79cd2469ca3d38f503a1a9e11.png)

1. ブラウザを起動し、プリザンターへログインできることを確認してください。