---
title: インストーラを利用したバージョンアップ手順(Azure App Service)
category: バージョンアップ(インストーラ)
order: '200'
status: ''
parts: ''
urlstring: version-up-installer-azure
translationKey: version-up-installer-azure
shortname: バージョンアップ手順,バージョンアップ手順（インストーラ）,インストーラ,App Serviceのバージョンアップ手順
created: 2024-11-27
updated: 2026-01-13
---

## 概要

 本手順は[インストーラ](../../installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)を使用してプリザンターをバージョンアップする手順です。インストーラを使用すると既存アプリケーションのバックアップ、最新バージョン資源のダウンロードやパラメータのマージなどを自動実行します。        
バックアップやモジュールの配置、パラメータのマージを手動で行う今までの手順でもバージョンアップ可能です。手動バージョンアップの手順は以下を参照ください。
[プリザンターのバージョンアップ手順(Azure App Service)](../version-up-manually/version-up-azure.md)

## 注意事項

1. インストーラを利用する場合、プリザンター 1.5へバージョンアップされます。プリザンター 1.4利用時は、スタック設定で.NET 10を指定してください。
1. Enterprise Editionにアップグレードし項目拡張を実施している場合は、[Enterprise Edition - バージョンアップ手順](../../../products-info/enterprise-edition/version-up/index.md)に従ってバージョンアップを実施してください。
1. Pleasanter Extensionsの[トライアル](../../../developers-guide/index.md)を実施中の場合は、本手順によるバージョンアップはできません。詳細は「Pleasanter Extensionsのトライアルの注意点」を確認してください。
1. <span class="pl-attention">**ver.1.4.17.0以降でインストーラによるアップデートおよびマージ機能をご利用の際は、[ver.1.4.17.0以降でマージ機能を利用する際の注意事項](https://pleasanter.org/ja/manual/version-up-ver1.4.17.0-caution)を確認してください。**</span>

## 制限事項

1. バージョンアップ元は1.4.0.0以降が対象です。
1. [インストーラ](../../installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)を使用したインストールはバージョンアップ元はVer1.4.0.0以降が対象です。Ver1.3.50.2以前をバージョンアップする際は手動バージョンアップの手順を参照ください。  
[プリザンターのバージョンアップ手順(Azure App Service)](../version-up-manually/version-up-azure.md)
1. バージョンアップ先は1.4.8.0以降が対象です。

## 手順

バージョンアップ手順は以下の通りです。
1. プリザンターの停止
1. データベースのバックアップ
1. インストーラのインストール
1. インストーラの実行
1. プリザンターの起動確認

## 1. プリザンターの停止

1. [Azure Portal](https://portal.azure.com/)に接続します。
2. App Service を開きます。
    ![Azure Portalの画面。App Serviceを開くところ](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/90ff8944d431483da62410cdf5f90100.png)
3. 作成済みの App Service インスタンスを選択します。
4. App Serviceを停止します。

## 2. データベースのバックアップ

データベースをバックアップします。**Enterprise Editionにアップグレードし、項目を拡張している場合は必ずバックアップしてください**
    [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)

## 3. インストーラのインストール

### 1. [Kudu](https://docs.microsoft.com/ja-jp/azure/app-service/resources-kudu#access-kudu-for-your-app) にアクセスします。

   1. App Service の左側のメニューの"開発ツール"から「高度なツール」をクリック
     ![App Serviceの左メニュー。「開発ツール」の中に「高度なツール」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/9e9a929cb8174c9f81ac9a25479890c4.png)
   2. 移動のリンクをクリック
      ![App Serviceの「高度なツール」画面。Kuduへの「移動」リンクがある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/8639e642c6ed4b07b1b86538b8394a9f.png)
   3. Kudu のヘッダメニューから「Debug console」>「CMD」をクリック
      ![Kuduのヘッダメニュー。「Debug console」の中に「CMD」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/8d9aeb33b8b94c62a787d8adca8360c8.png)
   4. インストーラをインストールします。（ご利用ユーザによってはD:\homeの場合もあります。その場合は適宜読み替えてください。）
    **インストール済みであっても必ず実行してください。インストーラがバージョンアップしている場合は更新インストールします。**
      1. [こちら](https://www.nuget.org/packages/Implem.PleasanterSetup/) からImplem.PleasanterSetupのNuget Galleryを開き、「Download package」より.nupkgファイルをダウンロードします。
![Implem.PleasanterSetupのNuGet Galleryのページ。「Download package」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/3566ffc5937a42f4b78b0e055375db87.png)
      2. 下記コマンドを実行してインストーラをインストールする任意のフォルダを作成します。  
      ※本手順では C:\home\dotnet-toolsを作成する場合として説明します。
          ```
          mkdir C:\home\dotnet-tools
          ```
      3. 2.3.1でダウンロードした.nupkgファイルをC:\home\dotnet-toolsに配置します。

      4. 下記コマンドを実行してインストーラをインストールします。
          ```
          dotnet tool install Implem.PleasanterSetup --tool-path C:\home\dotnet-tools --add-source C:\home\dotnet-tools
          set PATH=%PATH%;C:\home\dotnet-tools
          ```

## 4. インストーラの実行

1. 以下コマンドを実行して、インストーラを実行します。

     ```
     pleasanter-setup
     ```

2. プリザンターをインストールするディレクトリを入力します。  
    「C:\home\site\wwwroot」 にインストールする場合は、何も入力せずに Enter キーを押下します。
    ![インストーラの実行画面。プリザンターのインストール先を入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/c91404e6475b4800a769cfd28a6ebc52.png)

3. CodeDefinerをインストールするディレクトリを入力します。  
    「C:\home\site\CodeDefiner」 にインストールする場合は、何も入力せずに Enter キーを押下します。
    ![インストーラの実行画面。CodeDefinerのインストール先を入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/ffd86059eefd48fdbd283f8a730ffd44.png)

4. サマリ画面が表示されます。  
    内容を確認し、「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 」 の後に **y** を入力しEnterキーで実行してください。  
    ※パスワードはマスクされています。  
    ![インストーラのサマリ画面。内容を確認してyを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/cb9e41c53dd7476181d69a3786554d10.png)
    **※「y」を入力後、動作まで時間がかかる場合があります。ディレクトリを移動せずにお待ちください。**

5. 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力して実行してください。

    ```
    <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
    <SUCCESS> Starter.Main: All of the processes have been completed.
    Setup is complete.
    ```

6. セットアップが終了すると、Webブラウザが起動して[拡張コンテンツ(Pleasanter Extensions)トライアルの案内ページ](../../../developers-guide/index.md)が表示されます。

    ![セットアップ後に開くPleasanter Extensionsトライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/2f1b98e366bb4477bd5ab45e7d4aa8c0.png)

## 5. プリザンターの起動確認

1. App Serviceを開き、インスタンスを起動します。
1. ブラウザでプリザンターのログイン画面を開き、ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。
    ![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/0d80470fa83c40bd99c057d2447549e0.png)

※インストーラでバックアップされたC:\home\site\wwwroot_yyyyMMdd_HHmmssおよびC:\home\site\CodeDefiner_yyyyMMdd_HHmmssは不要な場合は削除してください。保存しておく場合は別フォルダに退避してください。
