---
title: インストーラを使ったトライアル開始
category: トライアル
order: '1100'
status: ''
parts: ''
urlstring: pleasanter-extensions-trial-installer-start
translationKey: pleasanter-extensions-trial-installer-start
shortname: インストーラを使ったトライアル開始
created: 2025-12-01
updated: 2025-12-03
---

## 概要

インストーラを使い[Pleasanter Extensionsトライアル](../../developers-guide/index.md)を開始する方法を説明します。

## 前提条件

1. 以下の手順では、プリザンターがインストール済みであることを前提とします。以下の手順では、プリザンターはインストールされないことに注意してください。
1. インストーラ使って[Pleasanter Extensionsトライアル](../../developers-guide/index.md)を開始するには、プリザンターが**バージョン1.4.15.0以降**である必要があります。

## 操作手順

各パスは、本ユーザマニュアルの手順に従ってインストールした場合の一例です。利用中の環境に応じて、適宜読み替えてください。

<div class="steps" markdown>

1.  以下のコマンドを実行し、最新のインストーラをインストールします。

    ``` text title="最新のインストーラをインストール"
    dotnet tool install -g Implem.PleasanterSetup
    ```

1.  `trial`オプションを付けてインストーラを実行します。

    ``` text title="trialオプションを付けてインストーラを実行"
    pleasanter-setup trial
    ```

1.  インストール先のディレクトリを指定します。変更する必要がなければ、++enter++ キーを押下してください。すると、インストール条件の概要（Summary）が表示されます。以下はWindowsの場合の一例です。

    ``` text title="インストール先のディレクトリを指定" hl_lines="1"
    Install Directory [Default: C:\web\pleasanter] :

    ------ Summary ------
    Install Directory         : C:\web\pleasanter
    DBMS                      : SQLServer
    SaConnectionString PWD    : **********
    OwnerConnectionString PWD : **********
    UserConnectionString PWD  : **********
    Server                    : localhost
    Service Name              : Implem.Pleasanter
    [Issues]
        Class       :
        Num         :
        Date        :
        Description :
        Check       :
        Attachments :
    [Results]
        Class       :
        Num         :
        Date        :
        Description :
        Check       :
        Attachments :
    ---------------------
    ```

1.  トライアルを開始するか確認されます。問題なければ ++y++ と入力し、++enter++ キーを押下してください。すると、CodeDefinerが呼び出され、現在のプリザンターについての情報が収集されます。

    ``` text title="トライアルの開始確認" hl_lines="2"
    Do you want to start the trial? Please enter ‘y(yes)' or 'n(no)’. :
    y
    <INFO> Starter.Main: Implem.CodeDefiner 1.4.22.0
    <INFO> Configurator.OutputLicenseInfo:
    ServerName: localhost
    Database: master
    Deadline: 0001/01/01
    Licensee:
    Users: 0
    <INFO> Configurator.OutputLicenseInfo: This edition is "Community Edition".
    ```

1.  続行するか尋ねられます。問題なければ ++y++ と入力し、++enter++ キーを押下してください。すると、トライアルのセットアップが開始されます。

    ``` text title="続行するかの確認" hl_lines="2"
    Type "y" (yes) to continue the Pleasanter Extensions Trial process, otherwise type "n" (no).
    y
    ```

1.  「Setup is complete.」と表示され、Webブラウザで[年間サポートサービスの案内ページ](https://pleasanter.org/extensions-trial-ended-info/?utm_source=installer&utm_medium=app&utm_campaign=extension-trial&utm_content=route03)が開きます。

    ``` text title="トライアル開始手順の完了" hl_lines="4"
        : （前略）
    <SUCCESS> Starter.TrialConfigureDatabase: Database configuration has been completed.
    <SUCCESS> Starter.Main: All of the processes have been completed.
    Setup is complete.
    ```

    ![年間サポートサービスの案内ページ](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/650164a728404348bca9e520d84a8d1a.png)

</div>

以上で、セットアップは完了です。続けて[トライアル開始の確認](trial-start-check.md)に進んでください。

## 関連情報

-   [Pleasanter Extensionsトライアル](../../developers-guide/index.md)
-   [年間サポートサービスの案内ページ](https://pleasanter.org/extensions-trial-ended-info/?utm_source=installer&utm_medium=app&utm_campaign=extension-trial&utm_content=route03)
-   [トライアル開始の確認](trial-start-check.md)
