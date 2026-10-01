---
title: インストーラでプリザンターをAzure App Serviceにサーバレス構成でインストールする
category: プリザンターのインストール(インストーラ)
order: '200'
status: ''
parts: ''
urlstring: getting-started-installer-pleasanter-azure
translationKey: getting-started-installer-pleasanter-azure
shortname: プリザンターのインストール,プリザンターのインストール（インストーラ）,インストーラ,App Serviceにインストール
created: 2024-11-26
updated: 2026-01-13
---

## 概要

本手順は[インストーラ](getting-started-installer-pleasanter-almalinux.md)を使用してプリザンターの動作環境を構築する手順です。モジュールの配置やパラメータ設定を手動で行う今までの手順でもインストール可能です。手動インストールの手順は以下を参照ください。
[プリザンターをAzure App Serviceにサーバレス構成でインストールする](../install-manually/getting-started-pleasanter-azure.md)

| 対象               | 環境・バージョン             |
| ------------------ | :--------------------------- |
| Web                | Microsoft Azure App Service   |
| DB                 | Microsoft Azure SQL Database |
| ランタイムスタック | .NET 10                      |
| Pleasanter | 1.5.0.0以降 |

## 制限事項

[インストーラ](getting-started-installer-pleasanter-almalinux.md)を使用したインストールはVer1.5.0.0以降が対象です。Ver1.4.23.3以前をインストールする際は手動インストールの手順を参照ください。
[プリザンターをAzure App Serviceにサーバレス構成でインストールする](../install-manually/getting-started-pleasanter-azure.md)

## 前提条件

1. Azure Portal へのログインが可能であること
1. Microsoft Azure App Service（Windows/.NET 10）が 1 インスタンス準備できている
1. Microsoft Azure SQL Database が 1 インスタンス準備できている
1. Microsoft Azure SQL Database の接続文字列が準備できている
1. Microsoft Azure SQL Database のファイアウォール設定で App Service および PC からの接続が許可されている

## 手順

構築手順は以下の通りです。

1. .NETの設定
1. インストーラのインストール
1. プリザンターのセットアップ
1. プリザンターの起動確認

## 1. .NET の設定

1. [Azure Portal](https://portal.azure.com/)に接続します。
1. App Service を開きます。
    ![Azure Portal で App Service を開いたところ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/90ff8944d431483da62410cdf5f90100.png)
1. 作成済みの App Service インスタンスを選択します。
1. 「構成」メニューの「全般設定」を開き、下図の通り設定します。
    ![App Service の「構成」の「全般設定」の画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/f7a1e2d947ee48d1b3b2ab0f74b763e6.png)  
    ![App Service の「全般設定」の画面。設定項目の続き](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/9bae32c89bc24b5cb915006f0d23464d.png)

    |番号|項目|設定内容|
    |:-:|:--|:--|
    |1|構成 (プレビュー)|クリックして選択します|
    |2|全般設定|クリックして選択します|
    |3|プラットフォーム|64bit|
    |4|FTPの状態|無効|
    |5|Always On|オン（※常時接続と表示されることがあります）|
    |6|スタック設定|クリックして選択します|
    |7|スタック|.NET|
    |8|.NETのバージョン|.NET 10 (LTS)

## 2. インストーラのインストール

1. App Service にてインスタンスを停止します。
1. [Kudu](https://docs.microsoft.com/ja-jp/azure/app-service/resources-kudu#access-kudu-for-your-app) にアクセスします。
   1. App Service の左側のメニューの"開発ツール"から「高度なツール」をクリック
     ![App Service の左メニューの「開発ツール」。「高度なツール」がある](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/9e9a929cb8174c9f81ac9a25479890c4.png)
   2. 移動のリンクをクリック
      ![高度なツール（Kudu）の画面。「移動」のリンクがある](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/8639e642c6ed4b07b1b86538b8394a9f.png)
   3. Kudu のヘッダメニューから「Debug console」>「CMD」をクリック
      ![Kudu のヘッダメニュー。「Debug console」から「CMD」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/8d9aeb33b8b94c62a787d8adca8360c8.png)
   4. インストーラをインストールします。（ご利用ユーザによってはD:\homeの場合もあります。その場合は適宜読み替えてください。）
      1. [こちら](https://www.nuget.org/packages/Implem.PleasanterSetup/) からImplem.PleasanterSetupのNuget Galleryを開き、「Download package」より.nupkgファイルをダウンロードします。
![Implem.PleasanterSetup の NuGet ギャラリーのページ。「Download package」がある](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/3566ffc5937a42f4b78b0e055375db87.png)
      1. 下記コマンドを実行してインストーラをインストールする任意のフォルダを作成します。  
      ※本手順では C:\home\dotnet-toolsを作成する場合として説明します。
          ```
          mkdir C:\home\dotnet-tools
          ```
      3. 2.4.1でダウンロードした.nupkgファイルをC:\home\dotnet-toolsに配置します。
      4. 下記コマンドを実行してインストーラをインストールします。
          ```
          dotnet tool install Implem.PleasanterSetup --tool-path C:\home\dotnet-tools --add-source C:\home\dotnet-tools
          ```
      5. パスを設定します。
          ```
          set PATH=%PATH%;C:\home\dotnet-tools
          ```

## 3. プリザンターのセットアップ

※インストーラを使用することで、最新バージョン資源を自動でダウンロードし、入力した値を元にService.json、Rds.jsonの値を自動設定します。

1. 以下コマンドを実行して、インストーラを実行します。

     ```
     pleasanter-setup
     ```

2. プリザンターをインストールするディレクトリを入力します。  
    「C:\home\site\wwwroot」 にインストールする場合は空白で Enter キーを押下してください。
    ![インストーラがプリザンターのインストール先ディレクトリを尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/46659c2b54c742dc9e5aeb5f5cd6d9a6.png)

3. CodeDefinerをインストールするディレクトリを入力します。  
    「C:\home\site\CodeDefiner」 にインストールする場合は空白で Enter キーを押下してください。
    ![インストーラが CodeDefiner のインストール先ディレクトリを尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/b8a1d7a4616b4fc5b7a872c680f6c88d.png)

4. サービス名を入力します。
    Azure で作成したデータベース名を入力してください。
    「Implem.Pleasanter」の場合は空白で Enter キーを押下してください。
    ![インストーラがサービス名を尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/ea914e6198a64929896e692a7b75b93b.png)

5. 接続文字列を入力します。
    ※ **Microsoft Azure SQL Database の接続文字列を全文入力してください。**
    ![インストーラが接続文字列を尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/c83469f26e20478982be1f0d8b114e95.png)

6. デフォルト言語を入力します。
    対応する言語の番号を入力してください。
    ![インストーラがデフォルト言語の番号を尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/641ecae4738f48759264e47203344901.png)

7. デフォルトのタイムゾーンを入力します。
    対応する言語の番号を入力してください。
    ![インストーラがデフォルトのタイムゾーンの番号を尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/cd3fc0ac4c304d8ca64b555bdf9e592b.png)

8. サマリ画面が表示されます。  
    入力した値に間違いがない場合は、「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 」 の後に **y** を入力しEnterキーで実行してください。  
    ※パスワードはマスクされています。  
    ![入力値を一覧にしたインストーラのサマリ画面。インストールするかを確認している](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/ce61dd3fe78446cf972c4bd5986b1308.png)

9. 実行後下記のようなログが流れます。

    ```
    Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 
    y
    Download Pleasanter
    Downloaded Pleasanter_1.5.0.0.zip to C:\home\site\Pleasanter_1.5.0.0.zip
    Start setting parameters
    Finish setting parameters
    <INFO> Starter.Main: Implem.CodeDefiner 1.5.0.0
    <INFO> Configurator.OutputLicenseInfo: 
    ServerName:
    Database:
    Deadline: 1/1/0001
    Licensee: 
    Users: 0
    <INFO> Configurator.OutputLicenseInfo: This edition is "Community Edition".
    Type "y" (yes) if the license is correct, otherwise type "n" (no).
    ```

10. 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力して実行してください。

    ```
    <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
    <SUCCESS> Starter.Main: All of the processes have been completed.
    Setup is complete.
    ```

11. セットアップが終了すると、Webブラウザが起動して[Enterprise Editionトライアルの案内ページ](../../../developers-guide/index.md)が表示されます。

       ![セットアップ完了後に Web ブラウザで表示される Enterprise Edition トライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/f300ef7558c5498fb6c2a44109ad601d.png)

## 4. プリザンターの起動確認

1. App Serviceにてインスタンスを起動します。

1. ブラウザでプリザンターのログイン画面を開き、「ログインID: Administrator」、「初期パスワード: pleasanter」を入力し、「ログイン」ボタンをクリックします。
    ![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/5477647dc121413190827affdc7fa1ff.png)

1. ログイン後に「Administrator」ユーザーのパスワード変更を求められるので、任意のパスワードを入力し、「変更」ボタンをクリックします。  
    ![初回ログイン後に表示される、Administrator のパスワード変更画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/d57262564d8e49568553a84b273d3797.png)