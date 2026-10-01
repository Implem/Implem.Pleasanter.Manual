---
title: CentOSに構築した以前のプリザンター(.NET Core版)からプリザンター 1.3以降への移行手順
category: 移行
order: '700'
status: ''
parts: ''
urlstring: migrate-to-pleasanter-centos
translationKey: migrate-to-pleasanter-centos
shortname: プリザンター 1.3への移行
created: 2021-07-03
updated: 2026-01-13
---

## 概要

本説明は、CentOSにインストールした.NET Core版のプリザンターをプリザンター 1.3へ移行するための手順です。

|対象|移行前|移行後|
|---|---|---|
|OS|CentOS|CentOS|
|DB|PostgreSQL|PostgreSQL|
|Webサーバ|Nginx|Nginx|
|Platform|.NET Core|.NET 6.0|
|Pleasanter|.NET Core版(1.1.〇.〇)|プリザンター 1.3(1.3.〇.〇)|

## 前提条件

CentOSにインストールした.NET Core版のプリザンターであることを確認してください。
1. プリザンターへログインしてください。

1. 画面右上にある「ヘルプ」より「バージョン」をクリックしてください。

1. バージョンが「1.1.〇.〇」であることを確認してください。

## 注意事項

1. 移行元の環境の設定ファイル(/web/pleasanter/Implem.Pleasanter/App_Data/Parametersディレクトリ配下)を編集している場合、移行先の環境へ上書きコピーしないでください。そのまま上書きすると**新しく追加になったパラメータが失われる**可能性がありますので、WinMerge等の差分ツールを使用して、変更部分のみを新しいパラメータファイルにマージしてください。この手順ではWinMergeを使用します。

## 事前準備

#### 使用ツール

1. ローカルPC(Windows)にWinSCP、WinMergeがインストールされていること。  
WinSCP：https://forest.watch.impress.co.jp/library/software/winscp/   
WinMerge：https://winmergejp.bitbucket.io/ 

#### データベースのバックアップ取得

1. プリザンターが導入されているサーバー（以降、リモートPC）へログインし、 以下のコマンドでプリザンターを停止してください。
```
# systemctl stop pleasanter
```

1. プリザンターのデータベースのバックアップを取得してください。  
[FAQ：PostgreSQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-postgresql-backup-restore.md)

## .NET6.0のインストール

1. リモートPCへログインし、以下のコマンドを実行してください。
```
# dnf update
# dnf install -y dotnet-sdk-6.0
```
1. 以下のコマンドでインストールできていることを確認してください。
```
# dotnet --version
```

## プリザンター 1.3のダウンロード

1. ブラウザを起動し、以下のURLへアクセスしてください。  
　https://pleasanter.org/dlcenter

1. 「プリザンター 1.3 Community Edition」の「プリザンター 1.3」をクリックし、ダウンロードしてください。

## モジュールの配置

1. ローカルPCでWinSCPを起動し、リモートPCへ接続してください。

1. ローカルPCに作業用フォルダ(C:\migration)、バックアップ用フォルダ(C:\migration\backup)を作成してください。

1. WinSCPでリモートPC側で「/web」ディレクトリへ移動してください。

1. リモートPC側の「/web/pleasanter」ディレクトリをローカルPC側の「C:\migration\backup」に退避してください。
![WinSCPでリモートの/web/pleasanterをローカルPCへ退避する画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/446988e542524e488b0b902aacaeec8e.png)  

1. リモートPC側の「/web/pleasanter」ディレクトリを削除してください。

1. ローカルPCの作業用フォルダにダウンロードしたファイルを展開してください。

1. WinMergeを起動し、以下の2つのフォルダを比較してください。  
　①C:\migration\pleasanter\Implem.Pleasanter\App_Data\Parameters  
　②C:\migration\backup\pleasanter\Implem.Pleasanter\App_Data\Parameters  
![WinMergeで新旧のParametersフォルダを比較した画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/86307f76da53485f8b670b7ae3a0abd0.png)  

1. 上記①のParametersフォルダ配下の各パラメータファイルを上記②のParametersフォルダ配下のものと比較しながら修正してください。  

![WinMergeでパラメータファイルの中身を比較しながら修正する画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/49f65685c4b14885a48cbc6a171521c7.png)  

1. WinSCPでローカルPCの「C:\migration\pleasanter」フォルダをリモートPCの「/web」ディレクトリへコピーしてください。
![WinSCPでローカルのpleasanterフォルダをリモートの/webへコピーする画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/19f1d0d2148944fc8938fcafe04e6c07.png)  

## プリザンターの起動

1. リモートPCにログインし、ターミナルを起動して、以下のコマンドを実行してください。
```
# cd /web/pleasanter/Implem.CodeDefiner
# dotnet Implem.CodeDefiner.dll _rds
```

1. 以下のコマンドでプリザンターを起動してください。
```
# systemctl start pleasanter
```

1. ブラウザを起動し、プリザンターへログインしてください。

1. 画面右上の「ヘルプ」より「バージョン」をクリックしてください。

1. バージョンが「1.3.〇.〇」になっていることを確認してください。

## その他

#### データベースの復元

データベースを復元する必要がある場合は下記ページを参考に実施ください。
[FAQ：PostgreSQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-postgresql-backup-restore.md)