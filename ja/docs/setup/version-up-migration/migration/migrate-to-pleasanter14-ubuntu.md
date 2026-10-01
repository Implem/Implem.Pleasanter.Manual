---
title: Ubuntuにインストールしたプリザンター 1.3をプリザンター 1.4へ移行する手順
category: 移行
order: '600'
status: ''
parts: ''
urlstring: migrate-to-pleasanter14-ubuntu
translationKey: migrate-to-pleasanter14-ubuntu
shortname: プリザンター 1.4への移行
created: 2021-07-14
updated: 2026-01-13
---

## 概要

Ubuntuにインストールした プリザンター 1.3 を プリザンター 1.4 へ移行するための手順です。他のディストリビューションにつきましては適宜読み替えていただくようお願いいたします。

|対象|移行前|移行後|
|---|---|---|
|OS|Ubuntu|Ubuntu|
|DB|PostgreSQL|PostgreSQL|
|Webサーバ|Nginx|Nginx|
|Platform|.NET 6.0|.NET 8.0|
|Pleasanter|プリザンター 1.3|プリザンター 1.4|

## 前提条件

1. プリザンターを起動するユーザが登録されていること。手順の中で記載している **<プリザンターを起動するユーザ>** はこのユーザを指します。

## 事前確認

Ubuntuにインストールしているプリザンターのバージョンを確認します。

1. プリザンターへログインします。
1. 画面右上にある「ヘルプ」より「バージョン」をクリックします。
1. バージョンが「1.3.〇.〇」であることを確認します。

## 注意事項

1. 移行元の環境の設定ファイル(/web/pleasanter/Implem.Pleasanter/App_Data/Parametersディレクトリ配下)を編集している場合、移行先の環境へ上書きコピーしないでください。そのまま上書きすると**新しく追加になったパラメータが失われる**可能性がありますので、WinMerge等の差分ツールを使用して、変更部分のみを新しいパラメータファイルにマージします。この手順ではWinMergeを使用します。

## 事前準備

#### 使用ツール

1. ローカルPC(Windows)にWinSCP、WinMergeがインストールされていること。  
WinSCP：https://forest.watch.impress.co.jp/library/software/winscp/   
WinMerge：https://winmergejp.bitbucket.io/  

#### データベースのバックアップ取得

1. プリザンターが導入されているサーバー（以降、サーバー）へログインし、 以下のコマンドでプリザンターを停止します。
```
sudo systemctl stop pleasanter
```

1.  プリザンターのデータベースのバックアップを取得します。  
[PostgreSQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-postgresql-backup-restore.md)

## .NET8.0のインストール

1. サーバーへログインし、以下のコマンドを実行します。
```
sudo wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
sudo chmod +x ./dotnet-install.sh
sudo ./dotnet-install.sh -c 8.0 -i /usr/local/bin
dotnet --version
```

詳細につきましては下記公式ページの **スクリプトでのインストール** をご参照ください。  
https://learn.microsoft.com/ja-jp/dotnet/core/install/linux-scripted-manual#scripted-install  

また、dotnetコマンドを実行した際に特定のファイルに関するエラーが発生するケースがございます。その際は下記ページをご参照ください。
https://learn.microsoft.com/ja-jp/dotnet/core/install/linux-package-mixup?pivots=os-linux-ubuntu

## プリザンター 1.4のダウンロード

1. ブラウザを起動し、以下のURLへアクセスします。  
　https://pleasanter.org/dlcenter

1. 「プリザンター 1.4 Community Edition」の「ダウンロード」をクリックし、ダウンロードします。

## モジュールの配置

1. ローカルPCでWinSCPを起動し、サーバーへ接続します。

2. ローカルPCに作業用フォルダ(C:\migration)、バックアップ用フォルダ(C:\migration\backup)を作成します。

3. WinSCPでサーバーの「/web」ディレクトリへ移動します。

4. サーバーの「/web/pleasanter」ディレクトリをローカルPCの「C:\migration\backup」に退避します。
![WinSCPでサーバーの/web/pleasanterをローカルPCへ退避する画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/446988e542524e488b0b902aacaeec8e.png)  

5. サーバーにログインし、サーバーの「/web/pleasanter」ディレクトリを削除します。

6. ローカルPCでダウンロードしたファイル(Pleasanter_1.4.x.x.zip)を「C:\migration」フォルダに展開します。

7. WinMergeを起動し、以下の2つのフォルダを比較します。
　①C:\migration\pleasanter\Implem.Pleasanter\App_Data\Parameters  
　②C:\migration\backup\pleasanter\Implem.Pleasanter\App_Data\Parameters  
![WinMergeで新旧のParametersフォルダを比較した画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/86307f76da53485f8b670b7ae3a0abd0.png)  

8. 上記①のParametersフォルダ配下の各パラメータファイルを上記②のParametersフォルダ配下のものと比較しながら修正します。
![WinMergeでパラメータファイルの中身を比較しながら修正する画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/49f65685c4b14885a48cbc6a171521c7.png)  

9. ローカルPCで「C:\migration\pleasanter」フォルダをzip圧縮します。※こちらの手順では「Pleasanter_1.4.x.x_merged.zip」という名前のzipファイルとします。

　　Pleasanter_1.4.x.x_merged.zip
　　　　└ pleasanter
　　　　　　├ Implem.CodeDefiner
　　　　　　└ Implem.Pleasanter

10. WinSCPで上記の「Pleasanter_1.4.x.x_merged.zip」をサーバーの作業用ユーザのホームディレクトリにコピーします。
![WinSCPでmergedのzipをサーバーのホームディレクトリへコピーする画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/2bec4947a0184b43b8498c7b9f57ef74.png)

## プリザンターの起動

1. サーバーにログインし、ホームディレクトリにある「Pleasanter_1.4.x.x_merged.zip」を 「/web」ディレクトリに 展開します。
```
sudo unzip Pleasanter_1.4.x.x_merged.zip -d /web
```

1. /web/pleasanter ディレクトリ配下の所有者をプリザンターを起動するユーザに変更します。
```
sudo chown -R <プリザンターを起動するユーザ> /web/pleasanter
```

1. プリザンターを起動するユーザでCodeDefinerを実行します。
```
cd /web/pleasanter/Implem.CodeDefiner
sudo -u <プリザンターを起動するユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds
```

1. プリザンターを起動します。
```
sudo systemctl start pleasanter
```

1. ブラウザを起動し、プリザンターへログインします。

1. 画面右上の「ヘルプ」より「バージョン」をクリックします。

1. バージョンが「1.4.〇.〇」になっていることを確認します。

## その他
#### データベースの復元
データベースを復元する必要がある場合は下記ページを参考に実施ください。
[PostgreSQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-postgresql-backup-restore.md)