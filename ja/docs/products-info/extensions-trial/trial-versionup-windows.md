---
title: 拡張コンテンツ(Pleasanter Extensions)トライアル中のバージョンアップ手順（Windows）
category: その他
order: '1700'
status: ''
parts: ''
urlstring: trial-versionup-windows
translationKey: trial-versionup-windows
shortname: ''
created: 2025-11-28
updated: 2026-01-13
---

## 概要

バージョン1.2.0以降のインストーラを使い、[Pleasanter Extensionsトライアル](index.md)（以下、トライアルと表記）実行中のプリザンターをバージョンアップする手順です。

バックアップやモジュールの配置、パラメータのマージを手動で行う今までの手順でもバージョンアップ可能です。手動バージョンアップの手順は以下を参照してください。

[プリザンターのバージョンアップ手順(Windows)](../../setup/version-up-migration/version-up-manually/version-up-net.md)

## 注意事項

1. <span class="pl-attention">**ver.1.4.17.0以降でインストーラによるアップデートおよびマージ機能をご利用の際は、[ver.1.4.17.0以降でマージ機能を利用する際の注意事項](https://pleasanter.org/ja/manual/version-up-ver1.4.17.0-caution)を確認してください。**</span>

## 制限事項

1.  インストーラを使用する場合、バージョンアップ元のプリザンターは、バージョン1.5.0.0以降が対象です。
1.  バージョン1.4.23.3以前のプリザンターをバージョンアップする際は、手動バージョンアップの手順を参照してください。
    [プリザンターのバージョンアップ手順(Windows)](../../setup/version-up-migration/version-up-manually/version-up-net.md)
1.  バージョンアップ先はバージョン1.4.8.0以降が対象です。
1.  `/e` オプションは使えません。

## 操作手順

## 1. プリザンターの停止

### 1. プリザンターの停止

1.  「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS)マネージャー」を起動してください。

1.  左ペインより「サーバー名」を選択します。右ペインの「停止」をクリックして、IISを停止してください。

    ![IISマネージャーでサーバー名を選び「停止」をクリックする画面](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/033a9ee7aa0841369709641c7d94b2bb.png)

## 2. データベースのバックアップ

データベースをバックアップします。バックアップの手順は以下の手順を参照してください。

[FAQ：バックアップ、リストア](../../FAQ/backup-restore/index.md)

## 3. インストーラのインストール／更新

**インストール済みであっても必ず実行してください。インストーラがバージョンアップしている場合は更新インストールします。**
下記コマンドを実行して、インストーラをインストールします。

``` bat
dotnet tool install -g Implem.PleasanterSetup
```

### ネットワーク環境に接続されていない場合は下記手順でインストールしてください。

<details markdown="1">
<summary>（こちらをクリックすると詳細が開閉します） </summary>

1.  下記コマンドを実行して.nupkgファイルを配置する任意のフォルダを作成します。
    ※本手順ではC:\dotnet-toolsを作成する場合として説明します。

    ``` bat
    mkdir C:\dotnet-tools
    ```

1.  [こちら](https://www.nuget.org/packages/Implem.PleasanterSetup/) からImplem.PleasanterSetupのNuget Galleryを開き、画像の①「Download package」より.nupkgファイルをダウンロードします。

    ![NuGet GalleryのImplem.PleasanterSetupのページ。①Download packageと②のコマンド](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/3ec2711d699e4c9eb1f978122e9bb5fc.png)

1.  手順2.2でダウンロードした.nupkgファイルを**C:\dotnet-tools**に配置します。
1.  画像の②のコマンドをコピーします。
1.  下記コマンド実行します。

    ``` bat
    <手順2.4でコピーしたコマンド> --add-source C:\dotnet-tools
    ```

    **例：Implem.PleasanterSetupのVersionが1.0.1の場合**

    ``` bat
    dotnet tool install --global Implem.PleasanterSetup --version 1.0.1 --add-source C:\dotnet-tools
    ```

</details>

## 4. インストーラの実行

※最新バージョンの資源およびParametersPatch.zipをダウンロードし、バージョンアップを実行します。

1.  以下コマンドを実行して、インストーラを実行します。

    ``` bat
    pleasanter-setup
    ```

    **ネットワーク環境に接続されていない場合は、下記手順を実施してください**

    ??? note "（こちらをクリックすると詳細が開閉します）"

        1.  [ダウンロードセンター](https://pleasanter.org/dlcenter)から最新バージョンのプリザンターをダウンロードし、「`C:\web\`」に配置します。

        1.  [GitHubのリリースページ](https://github.com/Implem/Implem.Pleasanter/releases)から、配置したバージョンと同様のParametersPatch.zipをダウンロードして「`C:\web\`」に配置します。

        1.  下記コマンドを実行します。  
            **`C:\web\`** ディレクトリ配下の構成が以下のようになっていることを確認してください。

            ``` text
            C:\web\Pleasanter_1.4.x.x.zip
            C:\web\ParametersPatch.zip
            ```

            ``` bat
            pleasanter-setup -r C:\web\Pleasanter_1.4.x.x.zip -patch C:\web\ParametersPatch.zip
            ```

1.  プリザンターがインストールされているディレクトリを入力します。  
    「C:\web\pleasanter」 にインストールされている場合は空白で Enter キーを押下します。

    ![プリザンターのインストール先ディレクトリを入力するプロンプト](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/3bb5261ce8ed46b690f5459d9580f8a2.png)

1.  サマリ画面が表示されます。  
    内容を確認し「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 」 の後に **y** を入力しEnterキーで実行してください。  
    ※パスワードはマスクされています。

    ![インストーラのサマリ画面](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/42b7cde127384f66b8d4f167761d599a.png)

1.  「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力して実行してください。

    ``` text
    <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
    <SUCCESS> Starter.Main: All of the processes have been completed.
    Setup is complete.
    ```

1.  バージョン1.1.2（Implem.PleasanterSetup.1.1.2.nupkg）以降のインストーラの場合、セットアップが終了すると、Webブラウザが起動して[拡張コンテンツ(Pleasanter Extensions)トライアルの案内ページ](../../developers-guide/index.md)が表示されます。

    ![セットアップ完了後にブラウザで表示されるトライアルの案内ページ](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/2f1b98e366bb4477bd5ab45e7d4aa8c0.png)

## 5. プリザンターの起動確認

1.  「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS）マネージャー」を起動します。

1.  左ペインより「サーバー名」を選択します。右ペインの「開始」をクリックして、IISを開始します。

    ![IISマネージャーでサーバー名を選び「開始」をクリックする画面](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/1fb50733a47b423591b1490ba1c8a272.png)

1.  開始後、左ペインより「サイト」-「Default Web Site」を選択し、右ペインの「*.80(http)参照」をクリックし、プリザンターを起動します。

    ![IISマネージャーでDefault Web Siteの「*.80(http)参照」をクリックする画面](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/5be4e5794d5941d2b31a51f81a26e0a4.png)

1.  ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。

    ![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/0d80470fa83c40bd99c057d2447549e0.png)

※インストーラでバックアップされたC:\web\pleasanter_yyyyMMdd_HHmmssは不要な場合は削除してください。保存しておく場合は別フォルダに退避してください。
