---
title: インストーラを利用したバージョンアップ手順(Linux)
category: バージョンアップ(インストーラ)
order: '300'
status: ''
parts: ''
urlstring: version-up-installer-linux
translationKey: version-up-installer-linux
shortname: バージョンアップ手順,バージョンアップ手順（インストーラ）,インストーラ,Linuxのバージョンアップ手順
created: 2024-11-27
updated: 2026-08-17
---

## 概要

本手順は[インストーラ](../../installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)を使用してプリザンターをバージョンアップする手順です。インストーラを使用すると既存アプリケーションのバックアップ、最新バージョン資源のダウンロードやパラメータのマージなどを自動実行します。バックアップやモジュールの配置、パラメータのマージを手動で行う今までの手順でもバージョンアップ可能です。手動バージョンアップの手順は以下を参照ください。
[プリザンターのバージョンアップ手順(Linux)](../version-up-manually/version-up-net-core.md)

## 注意事項

1. インストーラを利用する場合、プリザンター 1.5へバージョンアップされます。プリザンター 1.4利用時は、あらかじめ.NET10をインストールしてください。手順は「[インストーラでプリザンターをUbuntuにインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-ubuntu.md)」の「1. .NETのセットアップ」を参照してください。
1. Enterprise Editionにアップグレードし項目拡張を実施している場合は、[Enterprise Edition - バージョンアップ手順](../../../products-info/enterprise-edition/version-up/index.md)に従ってバージョンアップを実施してください。
1. Pleasanter Extensionsの[トライアル](../../../developers-guide/index.md)を実施中の場合は、本手順によるバージョンアップはできません。詳細は「Pleasanter Extensionsのトライアルの注意点」を確認してください。
1. <span class="pl-attention">**ver.1.4.17.0以降でインストーラによるアップデートおよびマージ機能をご利用の際は、[ver.1.4.17.0以降でマージ機能を利用する際の注意事項](https://pleasanter.org/ja/manual/version-up-ver1.4.17.0-caution)を確認してください。**</span>

## 制限事項

1. バージョンアップ元は1.4.0.0以降が対象です。
1. [インストーラ](../../installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)を使用したバージョンアップはバージョンアップ元はVer1.4.0.0以降が対象です。Ver1.3.50.2以前をバージョンアップする際は手動バージョンアップの手順を参照ください。  
[プリザンターのバージョンアップ手順(Linux)](../version-up-manually/version-up-net-core.md)
1. バージョンアップ先は1.4.8.0以降が対象です。

## 前提条件

1. プリザンターを起動するユーザが登録されていること。手順の中で記載している **<プリザンターを起動するユーザ>** はこのユーザを指します。
1. 本手順では.NETを /usr/local/bin にインストールする場合として説明します。同一環境に複数バージョンの.NETが必要などの理由で.NETを異なるディレクトリにインストールする場合は、CodeDefinerの実行時やPleasanterサービス用スクリプトの作成でExecStartに指定するディレクトリをインストール先に合わせて変更してください。

## 手順

バージョンアップ手順は以下の通りです。
1. プリザンターの停止
1. データベースのバックアップ
1. インストーラのインストール
1. インストーラの実行
1. プリザンターの起動確認

## 1. プリザンターの停止

以下コマンドを実行して、プリザンターを停止します。
```
sudo systemctl stop pleasanter
```

## 2. データベースのバックアップ

データベースをバックアップします。**Enterprise Editionにアップグレードし、項目を拡張している場合は必ずバックアップしてください**
    [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)

## 3. インストーラのインストール

**インストール済みであっても必ず実行してください。インストーラがバージョンアップしている場合は更新インストールします。**

以下コマンドを実行して、インストーラ をインストールします。

```
dotnet tool install -g Implem.PleasanterSetup
echo 'export PATH="$PATH:~/.dotnet/tools"' >> ~/.bashrc
echo 'export DOTNET_ROOT=/usr/local/bin' >> ~/.bashrc
echo 'export PATH=$PATH:$DOTNET_ROOT' >> ~/.bashrc
source ~/.bashrc
```

### ネットワーク環境に接続されていない場合は下記手順でインストールしてください。

<details markdown="1">
<summary>（こちらをクリックすると詳細が開閉します） </summary>

1. 下記コマンドを実行して.nupkgファイルを配置する任意のフォルダを作成します。
    ※本手順では/dotnet-toolsを作成する場合として説明します。
    ```
    sudo mkdir /dotnet-tools
    ```
1. [こちら](https://www.nuget.org/packages/Implem.PleasanterSetup/) からImplem.PleasanterSetupのNuget Galleryを開き、画像の①「Download package」より.nupkgファイルをダウンロードします。
    ![Implem.PleasanterSetupのNuGet Galleryのページ。①「Download package」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/3ec2711d699e4c9eb1f978122e9bb5fc.png)
1. 手順2.2でダウンロードした.nupkgファイルを**/dotnet-tools**に配置します。
1. 画像の②のコマンドをコピーします。
1. 下記コマンド実行します。

    ```
    <手順2.4でコピーしたコマンド> --add-source /dotnet-tools
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

## 4. インストーラの実行

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
            /web/Pleasanter_1.4.x.x.zip
            /web/ParametersPatch.zip
            ```

            ```
            pleasanter-setup -r /web/Pleasanter_1.4.x.x.zip -patch /web/ParametersPatch.zip
            ```

2. プリザンターをインストールするディレクトリを入力します。  
    「/web/pleasanter」 にインストールする場合は空白で Enter キーを押下してください。
    ![インストーラの実行画面。プリザンターのインストール先を入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/f13dfbf34ae042d3b0d29fc2a019868f.png)

3.  **<プリザンターを起動するユーザ>** を入力します。
    ![インストーラの実行画面。プリザンターを起動するユーザを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/e8c3b81488f54ab7ab82eb815a3cc292.png)

4. サマリ画面が表示されます。  
    内容を確認し、「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 」 の後に **y** を入力しEnterキーで実行してください。  
    ※パスワードはマスクされています。  
    ![インストーラのサマリ画面。内容を確認してyを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/ed79489a02c943278299da3894693ca0.png)

5. 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力して実行してください。

    ```
    <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
    <SUCCESS> Starter.Main: All of the processes have been completed.
    Setup is complete.
    ```

6. セットアップが終了すると、Webブラウザが起動してEnterprise Editionトライアルの案内ページが表示されます。

       ![セットアップ後に開くトライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/2f1b98e366bb4477bd5ab45e7d4aa8c0.png)

## 5. プリザンターの起動確認

1. 以下コマンドを実行して、プリザンターを起動します。

    ```
    sudo systemctl start pleasanter
    ```

2. ブラウザでプリザンターのログイン画面を開き、ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。
    ![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/0d80470fa83c40bd99c057d2447549e0.png)

※インストーラでバックアップされた/web/pleasanter_yyyyMMdd_HHmmssは不要な場合は削除してください。保存しておく場合は別フォルダに退避してください。
