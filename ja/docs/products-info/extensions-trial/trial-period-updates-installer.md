---
title: インストーラを使ったトライアル期間中のバージョンアップ
category: トライアル
order: '1500'
status: ''
parts: ''
urlstring: pleasanter-extensions-trial-notice
translationKey: pleasanter-extensions-trial-notice
shortname: プリザンターのバージョンアップとEnterprise Editionへのアップグレード
created: 2025-04-02
updated: 2025-12-03
---

## 概要

トライアル期間中にプリザンターをバージョンアップする方法を説明します。トライアル期間中のプリザンターのバージョンアップには、以下の2つの方法があります。

1. インストーラを使う方法
1. CodeDefinerを使う方法

このページでは、インストーラを使う方法を説明します。

!!! tip "CodeDefinerを使う方法"
    CodeDefinerを使う方法は、こちらを参照してください。

### インストーラを使う方法

1.  以下のコマンドを実行し、最新のインストーラをインストールしてください。

    ``` text
    dotnet tool install -g Implem.PleasanterSetup 
    ```

1.  以下のコマンドを実行し、インストーラを起動してください。

    ``` text
    pleasanter-setup
    ```

1.  インストール先のディレクトリを尋ねられます。既定の設定で構わない場合は、++enter++ キーを押下してください。

    ``` text title="Windowsでの実行例"
    Install Directory [Default: C:\web\pleasanter] :
    
    ```

1.  問題なければ ++y++ を入力し、++enter++ キーを押下してください。

    ``` text hl_lines="2"
    Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. :
    y
    ```

    CodeDefinerが呼び出され、項目の縮小が検知されると、自動的に`trial`オプションに切り替わります。

1.  `trial`オプションで続行する場合は ++y++ を入力し、++enter++ キーを押下してください。

    ``` text hl_lines="2"
    Type "y" (yes) to continue the Pleasanter Extensions Trial process, otherwise type "n" (no).
    y
    ```

    ここで ++n++ を選択した場合は、Webブラウザが起動し、[トライアルの案内ページ](../../developers-guide/index.md)が表示されます。

1.  「Setup is complete.」と表示されれば、トライアル期間中のバージョンアップは成功です。

    ``` text hl_lines="3"
    <SUCCESS> Starter.TrialConfigureDatabase: Database configuration has been completed.
    <SUCCESS> Starter.Main: All of the processes have been completed.
    Setup is complete.
    ```

!!! warning "トライアル期間が満了している場合"
    以下のように表示された場合は、トライアル期間が満了しています。

    ``` text
    <ERROR> Configurator. TrialConfigure: Trial period has expired. You can not rerun.
    <ERROR> Configurator. TrialConfigure: Database configuration canceled.
    ```

    Webブラウザで[Enterprise Editionの案内ページ](https://pleasanter.org/extensions-trial-ended-info/?utm_source=installer&utm_medium=app&utm_campaign=extension-trial&utm_content=route03)が開きますので、Enterprise Editionの導入をご検討ください。

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.4.15.0以降   | 機能追加 |

## 関連情報

-   [Pleasanter Extensionsのトライアル](../../developers-guide/index.md)
-   [トライアルの案内ページ](../../developers-guide/index.md)
-   [Enterprise Editionの案内ページ](https://pleasanter.org/extensions-trial-ended-info/?utm_source=installer&utm_medium=app&utm_campaign=extension-trial&utm_content=route03)
-   [手動バージョンアップ](../../setup/version-up-migration/version-up-manually/index.md)
-   [CodeDefinerのコマンド一覧](../../setup/codedefiner/codedefiner-command.md)
