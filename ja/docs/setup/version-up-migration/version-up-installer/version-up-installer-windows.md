---
title: インストーラを利用したバージョンアップ手順(Windows)
category: バージョンアップ(インストーラ)
order: '100'
status: ''
parts: ''
urlstring: version-up-installer-windows
translationKey: version-up-installer-windows
shortname: バージョンアップ手順,バージョンアップ手順（インストーラ）,インストーラ,Windowsのバージョンアップ手順
created: 2024-11-27
updated: 2026-09-08
---

**<span class="pl-attention">プリザンター1.5以降で、DBにSQL Serverを使用する場合は、必ず以下のマニュアルを確認してください。</span>**  
**[プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項](../../installation/prerequisites/sqlserver-connection-string-v15.md)**

## 概要

本手順は[インストーラ](../../installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)を使用してプリザンターをバージョンアップする手順です。インストーラを使用すると既存アプリケーションのバックアップ、最新バージョン資源のダウンロードやパラメータのマージなどを自動実行します。        
バックアップやモジュールの配置、パラメータのマージを手動で行う今までの手順でもバージョンアップ可能です。手動バージョンアップの手順は以下を参照ください。
[プリザンターのバージョンアップ手順(Windows)](../version-up-manually/version-up-net.md)

## 注意事項

1. インストーラを利用する場合、プリザンター 1.5へバージョンアップされます。現在プリザンター 1.4を利用されている場合は、[Windows/Windows Serverにインストールしたプリザンター 1.4をプリザンター 1.5へ移行する手順](../migration/migrate-to-pleasanter-windows.md)でプリザンター1.5へ移行してください。
1. Enterprise Editionにアップグレードし項目拡張を実施している場合は、[Enterprise Edition - バージョンアップ手順](../../../products-info/enterprise-edition/version-up/index.md)に従ってバージョンアップを実施してください。
1. Pleasanter Extensionsの[トライアル](../../../developers-guide/index.md)を実施中の場合は、本手順によるバージョンアップはできません。詳細は「Pleasanter Extensionsのトライアルの注意点」を確認してください。
1. <span class="pl-attention">**ver.1.4.17.0以降でインストーラによるアップデートおよびマージ機能をご利用の際は、[ver.1.4.17.0以降でマージ機能を利用する際の注意事項](https://pleasanter.org/ja/manual/version-up-ver1.4.17.0-caution)を確認してください。**</span>

## 制限事項

1. バージョンアップ元は1.4.0.0以降が対象です。
1. [インストーラ](../../installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)を使用したバージョンアップはバージョンアップ元はVer1.4.0.0以降が対象です。Ver1.3.50.2以前をバージョンアップする際は手動バージョンアップの手順を参照ください。  
[プリザンターのバージョンアップ手順(Windows)](../version-up-manually/version-up-net.md)
1. バージョンアップ先は1.4.8.0以降が対象です。

## 手順

バージョンアップ手順は以下の通りです。
1. プリザンターの停止
1. データベースのバックアップ
1. インストーラのインストール
1. インストーラの実行
1. プリザンターの起動確認

## 1. プリザンターの停止

1. 「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS)マネージャー」を起動してください。

1.  左ペインより「サーバー名」を選択します。右ペインの「停止」をクリックして、IISを停止してください。
![IISマネージャーの画面。右ペインの「停止」でIISを停止する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/033a9ee7aa0841369709641c7d94b2bb.png)

## 2. データベースのバックアップ

データベースをバックアップします。**Enterprise Editionにアップグレードし、項目を拡張している場合は必ずバックアップしてください**
    [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)

## 3. インストーラのインストール／更新

**インストール済みであっても必ず実行してください。インストーラがバージョンアップしている場合は更新インストールします。**
下記コマンドを実行して、インストーラをインストールします。
```
dotnet tool install -g Implem.PleasanterSetup
```

### ネットワーク環境に接続されていない場合は下記手順でインストールしてください。

<details markdown="1">
<summary>（こちらをクリックすると詳細が開閉します） </summary>

1. 下記コマンドを実行して.nupkgファイルを配置する任意のフォルダを作成します。
※本手順ではC:\dotnet-toolsを作成する場合として説明します。
```
mkdir C:\dotnet-tools
```
1. [こちら](https://www.nuget.org/packages/Implem.PleasanterSetup/) からImplem.PleasanterSetupのNuget Galleryを開き、画像の①「Download package」より.nupkgファイルをダウンロードします。
![Implem.PleasanterSetupのNuGet Galleryのページ。①「Download package」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/3ec2711d699e4c9eb1f978122e9bb5fc.png)
1. 手順2.2でダウンロードした.nupkgファイルを**C:\dotnet-tools**に配置します。
1. 画像の②のコマンドをコピーします。
1. 下記コマンド実行します。
```
<手順2.4でコピーしたコマンド> --add-source C:\dotnet-tools
```

 **例：Implem.PleasanterSetupのVersionが1.0.1の場合**

 ```
 dotnet tool install --global Implem.PleasanterSetup --version 1.0.1 --add-source C:\dotnet-tools
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

        1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から最新バージョンのプリザンターをダウンロードし、「`C:\web\`」に配置します。

        1. [GitHubのリリースページ](https://github.com/Implem/Implem.Pleasanter/releases)から、配置したバージョンと同様のParametersPatch.zipをダウンロードして「`C:\web\`」に配置します。

        1. 下記コマンドを実行します。  
           **`C:\web\`** ディレクトリ配下の構成が以下のようになっていることを確認してください。

            ```text
            C:\web\Pleasanter_1.4.x.x.zip
            C:\web\ParametersPatch.zip
            ```

            ```
            pleasanter-setup -r C:\web\Pleasanter_1.4.x.x.zip -patch C:\web\ParametersPatch.zip
            ```

2. プリザンターがインストールされているディレクトリを入力します。  
「C:\web\pleasanter」 にインストールされている場合は空白で Enter キーを押下します。
![インストーラの実行画面。プリザンターのインストール先を入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/3bb5261ce8ed46b690f5459d9580f8a2.png)

3. サマリ画面が表示されます。  
内容を確認し「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 」 の後に **y** を入力しEnterキーで実行してください。  
※パスワードはマスクされています。  
![インストーラのサマリ画面。内容を確認してyを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/42b7cde127384f66b8d4f167761d599a.png)

4. 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力して実行してください。
```
<SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
<SUCCESS> Starter.Main: All of the processes have been completed.
Setup is complete.
```

5. バージョン1.1.2（Implem.PleasanterSetup.1.1.2.nupkg）以降のインストーラの場合、セットアップが終了すると、Webブラウザが起動して[拡張コンテンツ(Pleasanter Extensions)トライアルの案内ページ](../../../developers-guide/index.md)が表示されます。

    ![セットアップ後に開くPleasanter Extensionsトライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/2f1b98e366bb4477bd5ab45e7d4aa8c0.png)

## 5. プリザンターの起動確認
1. 「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS）マネージャー」を起動します。

1.  左ペインより「サーバー名」を選択します。右ペインの「開始」をクリックして、IISを開始します。
![IISマネージャーの画面。右ペインの「開始」でIISを開始する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/1fb50733a47b423591b1490ba1c8a272.png)

1. 開始後、左ペインより「サイト」-「Default Web Site」を選択し、右ペインの「*.80(http)参照」をクリックし、プリザンターを起動します。
![IISマネージャー。「Default Web Site」の「*.80(http)参照」でプリザンターを開く](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/5be4e5794d5941d2b31a51f81a26e0a4.png)

1. ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。
![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-installer/assets/90216f28aecd46569e503dd5b7a66798.png)

※インストーラでバックアップされたC:\web\pleasanter_yyyyMMdd_HHmmssは不要な場合は削除してください。保存しておく場合は別フォルダに退避してください。
