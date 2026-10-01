---
title: Azure App Serviceにインストールしたプリザンター1.4をプリザンター1.5へ移行する手順
category: 移行
order: '400'
status: ''
parts: ''
urlstring: migrate-to-pleasanter-appservice
translationKey: migrate-to-pleasanter-appservice
shortname: ''
created: 2026-01-07
updated: 2026-01-13
---

## 概要

Azure App Serviceにインストールしたプリザンター 1.4をプリザンター1.5に移行するための手順です。

| 対象 | 移行前 | 移行後 |
| ----- | ------ | ------ |
| Web | App Service | App Service |
| DB | SQL Database | SQL Database |
| Platform | .NET8.0 | .NET10.0 |
| Pleasanter |プリザンター1.4 | プリザンター1.5 |

## 事前確認

App Serviceにインストールしているプリザンターのバージョンを確認します。

1. プリザンターへログインしてください。
1. ナビゲーションメニューの「ヘルプ」をクリックしてください。
1. 「バージョン」をクリックしてください。
1. バージョンが「1.4.〇.〇」であることを確認してください。

## 事前準備

### データベースのバックアップ取得

データベースをバックアップします。**Enterprise Editionにアップグレードし、項目を拡張している場合は必ずバックアップしてください**
[Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)

## 1. スタック設定の変更

1. App Service を開きます。
1. 作成済みの App Service インスタンスを選択します。
1. 「設定」－「構成 (プレビュー)」と選択し、「スタック設定」タブを開きます。「スタック」で[.NET](../../installation/install-dotnet/install-dotnet-windows.md)を選択し、「.NETのバージョン」で「.NET 10 (LTS)」を選択します。
    ![App Serviceの「構成 (プレビュー)」の「スタック設定」タブ。.NETのバージョンを選ぶ](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/ab169fd89b4a4b31a2aa7ab8fc995a7a.png)

## 2. インストーラのインストール／更新

**インストール済みであっても必ず実行してください。インストーラがバージョンアップしている場合は更新インストールします。**

1. App Service の左側のメニューの「開発ツール」から「高度なツール」を選択してください。

       ![App Serviceの左メニュー。「開発ツール」の中に「高度なツール」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/9e9a929cb8174c9f81ac9a25479890c4.png)

2. 移動のリンクをクリックし、[Kudu](https://docs.microsoft.com/ja-jp/azure/app-service/resources-kudu#access-kudu-for-your-app) にアクセスしてください。

       ![App Serviceの「高度なツール」画面。Kuduへの「移動」リンクがある](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/8639e642c6ed4b07b1b86538b8394a9f.png)

3. Kuduのヘッダメニューから「Debug console」－「CMD」を選択してください。

       ![Kuduのヘッダメニュー。「Debug console」の中に「CMD」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/8d9aeb33b8b94c62a787d8adca8360c8.png)

4. 以下のコマンドを実行し、.nupkgファイルを配置するフォルダを作成してください。  
    本手順では C:\home\dotnet-toolsを作成する場合として説明します。（ご利用ユーザによってはD:\homeの場合もあります。その場合は適宜読み替えてください。）

       ```
       mkdir C:\home\dotnet-tools
       ```

5. [こちら](https://www.nuget.org/packages/Implem.PleasanterSetup/) からImplem.PleasanterSetupのNuget Galleryを開き、画像の「Download package」より.nupkgファイルをダウンロードしてください。

       ![Implem.PleasanterSetupのNuGet Galleryのページ。「Download package」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/9703be9deb924691807402e477c37a9f.png)

6. 手順5でダウンロードした.nupkgファイルを**C:\home\dotnet-tools**に配置してください。

7. 以下のコマンドを実行してください。

       ```
       dotnet tool install Implem.PleasanterSetup --tool-path C:\home\dotnet-tools --add-source C:\home\dotnet-tools
       set PATH=%PATH%;C:\home\dotnet-tools
       ```

## 3. インストーラの実行

※最新バージョンの資源およびParametersPatch.zipをダウンロードし、バージョンアップを実行します。

1. 以下コマンドを実行して、インストーラを実行します。

       ```
       pleasanter-setup
       ```

2. プリザンターがインストールされているディレクトリを入力してください。  
       「C:\home\site\wwwroot」 にインストールする場合は、何も入力せずに Enter キーを押下してください。  
       ![インストーラの実行画面。プリザンターのインストール先を入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/c91404e6475b4800a769cfd28a6ebc52.png)

3. CodeDefinerをインストールするディレクトリを入力します。  
       「C:\home\site\CodeDefiner」にインストールする場合は、何も入力せずに Enter キーを押下してください。  
       ![インストーラの実行画面。CodeDefinerのインストール先を入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/ffd86059eefd48fdbd283f8a730ffd44.png)

4. サマリ画面が表示されます。  
       内容を確認し、「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 」 の後に **y** を入力しEnterキーで実行してください。  
       ※パスワードはマスクされています。  
       ![インストーラのサマリ画面。内容を確認してyを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/cb9e41c53dd7476181d69a3786554d10.png)  
       **※「y」を入力後、動作まで時間がかかる場合があります。ディレクトリを移動せずにお待ちください。**

5. 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力して実行してください。

       ```
       <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
       <SUCCESS> Starter.Main: All of the processes have been completed.
       Setup is complete.
       ```

6. セットアップが終了すると、Webブラウザが起動して[拡張コンテンツ(Pleasanter Extensions)トライアルの案内ページ](../../../developers-guide/index.md)が表示されます。
    ![セットアップ後に開くPleasanter Extensionsトライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/2f1b98e366bb4477bd5ab45e7d4aa8c0.png)

## 4. プリザンターの起動

1. App Serviceを開き、インスタンスを起動します。
1. ブラウザを起動し、プリザンターへログインしてください。
1. ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。
       ![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/0d80470fa83c40bd99c057d2447549e0.png)

※インストーラでバックアップされたC:\home\site\wwwroot_yyyyMMdd_HHmmssおよびC:\home\site\CodeDefiner_yyyyMMdd_HHmmssは不要な場合は削除してください。保存しておく場合は別フォルダに退避してください。