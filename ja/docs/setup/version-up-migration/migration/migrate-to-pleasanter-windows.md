---
title: Windows/Windows Serverにインストールしたプリザンター 1.4をプリザンター 1.5へ移行する手順
category: 移行
order: '100'
status: ''
parts: ''
urlstring: migrate-to-pleasanter-windows
translationKey: migrate-to-pleasanter-windows
shortname: プリザンター 1.5への移行
created: 2026-01-05
updated: 2026-01-13
---

## 概要

Windows Serverにインストールされているプリザンターをプリザンター 1.5に移行するための手順です。

| 対象       | 移行前                 | 移行後                 |
| ---------- | ---------------------- | ---------------------- |
| OS         | Windows/Windows Server | Windows/Windows Server |
| DB         | SQL Server             | SQL Server             |
| Webサーバ  | IIS                    | IIS                    |
| Platform   | .NET 8.0               | .NET 10.0              |
| Pleasanter | プリザンター 1.4       | プリザンター 1.5       |

**<span class="pl-attention">プリザンター1.5以降で、DBにSQL Serverを使用する場合は、必ず以下のマニュアルを確認してください。</span>**  
**[プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項](../../installation/prerequisites/sqlserver-connection-string-v15.md)**

## 注意事項

1. 本手順を実施する前にシステムのバックアップおよびデータベースのバックアップを取得してください。

## 事前確認

Windows/Windows Serverにインストールしているプリザンターのバージョンを確認します。

1. プリザンターへログインしてください。
1. ナビゲーションメニューの「ヘルプ」をクリックしてください。
1. 「バージョン」をクリックしてください。
1. バージョンが「1.4.〇.〇」であることを確認してください。

## 事前準備

#### データベースのバックアップ取得（Windows Serverの場合）

1. 「サーバーマネージャー」の「ツール」メニューを開き「インターネット インフォメーション サービス（IIS) マネージャー」を起動してください。

1. 左ペインでサーバ名を選択し、右ペインの「停止」をクリックし、IISを停止してください。  
   ![IISマネージャーの画面。右ペインの「停止」でIISを停止する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/79ffe4e682fc49c9abe8be89508b4e63.png)

1. プリザンターのデータベースのバックアップを取得してください。  
   [FAQ：プリザンターのDBデータを定期的にバックアップしたい（SQL Server）](../../../FAQ/backup-restore/faq-backup-schedule.md)

## .NET 10.0のインストール

!!! warning
    .NET 10.0の「SDK 10.0.x」と「Hosting Bundle」の2つをインストールしてください。

## 手順

.NETのインストール手順は以下の通りです。

1.  SDKのインストール
1.  Hosting Bundleのインストール

## SDKのインストール

1. ブラウザを起動し、以下のURLへアクセスしてください。  
　https://dotnet.microsoft.com/download/dotnet/10.0

1. 「SDK 10.0.x」をダウンロードし、インストールしてください。
![image](https://pleasanter.org/files/images/ja/setup/installation/install-dotnet/assets/3908c21830a949b1a41220b880c362ec.png)

1. コマンドプロンプトまたはPowerShellを起動して以下のコマンドを実行し、「10.0.x」が表示されることを確認してください。
```
 dotnet --version
```

## Hosting Bundleのインストール

1. 「Hosting Bundle」をダウンロードし、インストールしてください。
![image](https://pleasanter.org/files/images/ja/setup/installation/install-dotnet/assets/d4b3ffde58e14e91bcd1c416f31b9db3.png)

## インストーラのインストール／更新

**インストール済みであっても必ず実行してください。インストーラがバージョンアップしている場合は更新インストールします。**

下記コマンドを実行して、インストーラをインストールしてください。

```
dotnet tool install -g Implem.PleasanterSetup
```

インターネットに接続されていない場合は、以下の手順でインストールしてください。

<details markdown="1">
<summary>（こちらをクリックすると詳細が開閉します）</summary>

1. 以下のコマンドを実行し、.nupkgファイルを配置する任意のフォルダを作成してください。  
   ※本手順ではC:\dotnet-toolsを作成する場合を例に説明します。
   ```
   mkdir C:\dotnet-tools
   ```
1. [こちら](https://www.nuget.org/packages/Implem.PleasanterSetup/) からImplem.PleasanterSetupのNuget Galleryを開き、画像の①「Download package」より.nupkgファイルをダウンロードしてください。  
   ![Implem.PleasanterSetupのNuGet Galleryのページ。①「Download package」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/3ec2711d699e4c9eb1f978122e9bb5fc.png)
1. 手順2でダウンロードした.nupkgファイルを**C:\dotnet-tools**に配置してください。
1. 画像の②のコマンドをコピーしてください。
1. 以下のコマンドを実行してください。
   ```
   <手順2.4でコピーしたコマンド> --add-source C:\dotnet-tools
   ```
    **例：Implem.PleasanterSetupのVersionが1.0.1の場合**
    ```
    dotnet tool install --global Implem.PleasanterSetup --version 1.0.1 --add-source C:\dotnet-tools
    ```
</details>

## インストーラの実行

※最新バージョンの資源およびParametersPatch.zipをダウンロードし、バージョンアップを実行します。

1. 以下コマンドを実行して、インストーラを実行してください。

    ```
    pleasanter-setup
    ```

    **ネットワーク環境に接続されていない場合は、下記手順を実施してください。**

    ??? note "（こちらをクリックすると詳細が開閉します）"

        1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から最新バージョンのプリザンターをダウンロードし、「`C:\web\`」に配置してください。

        1. [GitHubのリリースページ](https://github.com/Implem/Implem.Pleasanter/releases)から、配置したバージョンと同様のParametersPatch.zipをダウンロードして「`C:\web\`」に配置してください。

        1. 下記コマンドを実行してください。  
           **`C:\web\`**ディレクトリ配下の構成が以下のようになっていることを確認してください。

            ```text
            C:\web\Pleasanter_1.5.x.x.zip
            C:\web\ParametersPatch.zip
            ```

            ```
            pleasanter-setup -r C:\web\Pleasanter_1.5.x.x.zip -patch C:\web\ParametersPatch.zip
            ```

2. プリザンターがインストールされているディレクトリを入力してください。  
「C:\web\pleasanter」 にインストールされている場合は、何も入力せずにEnterキーを押下してください。
![インストーラの実行画面。プリザンターのインストール先を入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/3bb5261ce8ed46b690f5459d9580f8a2.png)

3. サマリ画面が表示されます。  
内容を確認し「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 」 の後に **y** を入力しEnterキーで実行してください。  
※パスワードはマスクされています。  
![インストーラのサマリ画面。内容を確認してyを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/42b7cde127384f66b8d4f167761d599a.png)

4. 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力して実行してください。
```
<SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
<SUCCESS> Starter.Main: All of the processes have been completed.
Setup is complete.
```

5. セットアップが終了すると、Webブラウザが起動して[拡張コンテンツ(Pleasanter Extensions)トライアルの案内ページ](../../../developers-guide/index.md)が表示されます。
   ![セットアップ後に開くPleasanter Extensionsトライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/2f1b98e366bb4477bd5ab45e7d4aa8c0.png)

## 接続文字列の確認

開発環境など、TLSサーバ証明書が設定されていないSQL Serverをデータベースとして使用する場合、各接続情報の末尾へTrustServerCertificate=True;を追加してください。

##### RDS.json（該当部分を抜粋）

```
    "SaConnectionString": "Server=(local);Database=master;UID=sa;PWD=<SQL Serverのsaアカウントのパスワード>;Connection Timeout=30;TrustServerCertificate=true;",
    "OwnerConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=<任意のパスワード>;Connection Timeout=30;TrustServerCertificate=true;",
    "UserConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_User;PWD=<任意のパスワード>;Connection Timeout=30;TrustServerCertificate=true;",
```

詳細は「プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項」を確認してください。

## プリザンターの起動

1. 「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS）マネージャー」を起動してください。

1.  左ペインより「サーバー名」を選択してください。右ペインの「開始」をクリックして、IISを開始してください。
![IISマネージャーの画面。右ペインの「開始」でIISを開始する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/1fb50733a47b423591b1490ba1c8a272.png)

1. 開始後、左ペインより「サイト」-「Default Web Site」を選択し、右ペインの「*.80(http)参照」をクリックし、プリザンターを起動してください。
![IISマネージャー。「Default Web Site」の「*.80(http)参照」でプリザンターを開く](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/5be4e5794d5941d2b31a51f81a26e0a4.png)

1. ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認してください。
![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/90216f28aecd46569e503dd5b7a66798.png)