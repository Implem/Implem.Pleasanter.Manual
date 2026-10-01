---
title: Ubuntuにインストールしたプリザンター 1.4をプリザンター 1.5へ移行する手順
category: 移行
order: '500'
status: ''
parts: ''
urlstring: migrate-to-pleasanter-ubuntu
translationKey: migrate-to-pleasanter-ubuntu
shortname: プリザンター 1.5への移行
created: 2026-01-06
updated: 2026-01-13
---

## 概要

Ubuntuにインストールしたプリザンター 1.4をプリザンター 1.5へ移行するための手順です。他のディストリビューションにつきましては適宜読み替えていただくようお願いいたします。

| 対象       | 移行前           | 移行後           |
| ---------- | ---------------- | ---------------- |
| OS         | Ubuntu           | Ubuntu           |
| DB         | PostgreSQL       | PostgreSQL       |
| Webサーバ  | Nginx            | Nginx            |
| Platform   | .NET 8.0         | .NET 10.0        |
| Pleasanter | プリザンター 1.4 | プリザンター 1.5 |

## 前提条件

1. プリザンターを起動するユーザが登録されていること。手順の中で記載している **<プリザンターを起動するユーザ>** はこのユーザを指します。
1. 本手順では.NETを /usr/local/bin にインストールする場合として説明します。同一環境に複数バージョンの.NETが必要などの理由で.NETを異なるディレクトリにインストールする場合は、CodeDefinerの実行時やPleasanterサービス用スクリプトの作成でExecStartに指定するディレクトリをインストール先に合わせて変更してください。

## 事前確認

Ubuntuにインストールしているプリザンターのバージョンを確認します。

1. プリザンターへログインしてください。
1. 画面右上にある「ヘルプ」より「バージョン」をクリックしてください。
1. バージョンが「1.4.〇.〇」であることを確認してください。

## 事前準備

### データベースのバックアップ取得

1. プリザンターが導入されているサーバー（以降、サーバー）へログインし、 以下のコマンドでプリザンターを停止してください。
   ```
   sudo systemctl stop pleasanter
   ```
1.  プリザンターのデータベースのバックアップを取得してください。  
   [PostgreSQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-postgresql-backup-restore.md)

## 1. .NET 10.0のインストール

1. サーバーへログインし、以下のコマンドを実行してください。
   ```
   sudo wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
   sudo chmod +x ./dotnet-install.sh
   sudo ./dotnet-install.sh -c 10.0 -i /usr/local/bin
   dotnet --version
   ```
   上から3行目のコマンドで、.NETのインストール先を/usr/local/bin以外に変更した場合は、CodeDefinerの実行時やPleasanterサービス用スクリプトの作成でExecStartに指定するディレクトリをインストール先に合わせて変更してください。

   詳細は以下の**スクリプトでのインストール**をご参照ください。  
   https://learn.microsoft.com/ja-jp/dotnet/core/install/linux-scripted-manual#scripted-install  

   また、dotnetコマンドを実行した際に特定のファイルに関するエラーが発生するケースがあります。その際は以下を参照してください。  
   https://learn.microsoft.com/ja-jp/dotnet/core/install/linux-package-mixup?pivots=os-linux-ubuntu

## 2. インストーラのインストール／更新

**インストール済みであっても必ず実行してください。インストーラがバージョンアップしている場合は更新インストールします。**

以下のコマンドを実行して、インストーラをインストールしてください。

```
dotnet tool install -g Implem.PleasanterSetup
echo 'export PATH="$PATH:~/.dotnet/tools"' >> ~/.bashrc
echo 'export DOTNET_ROOT=/usr/local/bin' >> ~/.bashrc
echo 'export PATH=$PATH:$DOTNET_ROOT' >> ~/.bashrc
source ~/.bashrc
```

インターネットに接続されていない場合は、以下の手順でインストールしてください。

<details markdown="1">

<summary>（こちらをクリックすると詳細が開閉します）</summary>

1. 以下のコマンドを実行し、.nupkgファイルを配置するフォルダを作成してください。  
本手順では/dotnet-toolsを作成する場合を例に説明します。
   ```
   sudo mkdir /dotnet-tools
   ```
1. [こちら](https://www.nuget.org/packages/Implem.PleasanterSetup/)からImplem.PleasanterSetupのNuget Galleryを開き、画像の①「Download package」より.nupkgファイルをダウンロードしてください。  
![Implem.PleasanterSetupのNuGet Galleryのページ。①「Download package」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/3ec2711d699e4c9eb1f978122e9bb5fc.png)
1. 手順2でダウンロードした.nupkgファイルを**/dotnet-tools**に配置してください。
1. 画像の②のコマンドをコピーしてください。
1. 以下のコマンドを実行してください。
   ```
   <手順4でコピーしたコマンド> --add-source /dotnet-tools
   echo 'export PATH="$PATH:~/.dotnet/tools"' >> ~/.bashrc
   echo 'export DOTNET_ROOT=/usr/local/bin' >> ~/.bashrc
   echo 'export PATH=$PATH:$DOTNET_ROOT' >> ~/.bashrc
   source ~/.bashrc
   ```
   **例：Implem.PleasanterSetupのVersionが1.0.1の場合**
   ```
   dotnet tool install --global Implem.PleasanterSetup --version 1.0.1 --add-source /dotnet-tools
   echo 'export PATH="$PATH:~/.dotnet/tools"' >> ~/.bashrc
   echo 'export DOTNET_ROOT=/usr/local/bin' >> ~/.bashrc
   echo 'export PATH=$PATH:$DOTNET_ROOT' >> ~/.bashrc
   source ~/.bashrc
   ```
</details>

## 3. インストーラの実行

※最新バージョンの資源およびParametersPatch.zipをダウンロードし、バージョンアップを実行します。

1. 以下コマンドを実行して、インストーラを実行します。

    ```
    pleasanter-setup
    ```

    **ネットワーク環境に接続されていない場合は、下記手順を実施してください**

    ??? note "（こちらをクリックすると詳細が開閉します）"

        1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から最新バージョンのプリザンターをダウンロードし、「/web/」に配置します。

        1. [GitHubのリリースページ](https://github.com/Implem/Implem.Pleasanter/releases)から、配置したバージョンと同様のParametersPatch.zipをダウンロードして「/web/」に配します

        1. 下記コマンドを実行します。  
           **/web/** ディレクトリ配下の構成が以下のようになっていることを確認してください。

            ```text
            /web/Pleasanter_1.5.x.x.zip
            /web/ParametersPatch.zip
            ```

            ```
            pleasanter-setup -r /web/Pleasanter_1.5.x.x.zip -patch /web/ParametersPatch.zip
            ```

1. プリザンターがインストールされているディレクトリを入力してください。  
   「/web/pleasanter」にインストールする場合は、何も入力せずにEnterキーを押下してください。  
   ![インストーラの実行画面。プリザンターのインストール先を入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/f13dfbf34ae042d3b0d29fc2a019868f.png)

1.  **<プリザンターを起動するユーザ>**を入力してください。  
   ![インストーラの実行画面。プリザンターを起動するユーザを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/e8c3b81488f54ab7ab82eb815a3cc292.png)

1. サマリ画面が表示されます。  
内容を確認し、「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 」 の後に **y** を入力しEnterキーで実行してください。  
※パスワードはマスクされています。  
![インストーラのサマリ画面。内容を確認してyを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/ed79489a02c943278299da3894693ca0.png)

1. 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力して実行してください。
```
<SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
<SUCCESS> Starter.Main: All of the processes have been completed.
Setup is complete.
```

1. セットアップが終了すると、Webブラウザが起動し[拡張コンテンツ(Pleasanter Extensions)トライアルの案内ページ](https://pleasanter.org/pleasanter-extensions-trial/?utm_source=installer&utm_medium=app&utm_campaign=extension-trial&utm_content=route01&_gl=1*8uyahl*_ga*MTM3OTgwMzk2My4xNzYwNjg2Mzc2*_ga_FHETHGLQJE*czE3Njc4MzEwMDckbzEyNSRnMSR0MTc2NzgzODgxMyRqNjAkbDAkaDA.)が表示されます。  

   ![セットアップ後に開くPleasanter Extensionsトライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/2f1b98e366bb4477bd5ab45e7d4aa8c0.png)

## 4. プリザンターの起動

1. プリザンターを起動してください。
   ```
   sudo systemctl start pleasanter
   ```
1. ブラウザを起動し、プリザンターへログインしてください。
1. ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。

   ![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/90216f28aecd46569e503dd5b7a66798.png)

## 5. その他

#### データベースの復元

データベースを復元する必要がある場合は下記ページを参考に実施ください。

[PostgreSQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-postgresql-backup-restore.md)