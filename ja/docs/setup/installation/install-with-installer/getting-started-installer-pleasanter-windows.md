---
title: インストーラでプリザンターをWindowsにインストールする
category: プリザンターのインストール(インストーラ)
order: '100'
status: ''
parts: ''
urlstring: getting-started-installer-pleasanter-windows
translationKey: getting-started-installer-pleasanter-windows
shortname: ''
authors:
    - 'KIZU Shigeru'
    - 'MINE Haruka'
created: 2024-11-26
updated: 2026-09-08
---

## 概要

本手順はインストーラを使用してプリザンターの動作環境を構築する手順です。モジュールの配置やパラメータ設定を手動で行う今までの手順でもインストール可能です。手動インストールの手順は以下を参照ください。

-   [プリザンターをWindowsにインストールする](../install-manually/getting-started-pleasanter-windows.md)

|対象|環境・バージョン|
|:--|:--|
|OS|Windows Server|
|DB|SQL Server、PostgreSQL、MySQLのいずれか|
|Webサーバ|IIS|
|Platform|.NET 10|
|Pleasanter|1.5.0.0以降|

プリザンター1.5以降で、DBにSQL Serverを使用する場合は、必ず以下のマニュアルを確認してください。

-   プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項

## 注意事項

1.  ver1.4.6以降でのインストール時に、CodeDefinerに引数を指定しないで実行した場合、言語：英語、タイムゾーン：UTCでセットアップされますので、必要に応じて言語とタイムゾーンをご指定ください。
1.  MySQLはver1.4.9.0以降で使用できます。ver1.4.9.0より前のプリザンターはMySQLに対応していません。
1.  MySQLにおいてWebサーバとDBサーバを分離した構成にする場合は「WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）」または「WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）」を参照ください。

## 制限事項

インストーラを使用したインストールはVer1.5.0.0以降が対象です。Ver1.4.23.3以前をインストールする際は手動インストールの手順を参照ください。

-   [プリザンターをWindowsにインストールする](../install-manually/getting-started-pleasanter-windows.md)

## :one: 事前準備

以下のマニュアルに書かれている事前準備を済ませてください。

-   [プリザンターをWindowsにインストールする際の事前準備](../install-manually/getting-preparation-pleasanter-windows.md)

## :two: インストーラのインストール

インストーラをインストールします。以下のコマンドを実行してください。

``` ps1
dotnet tool install -g Implem.PleasanterSetup
```

## :three: プリザンターのセットアップ

インストーラは、最新バージョン資源を自動でダウンロードし、入力した値を元に[Service.json](../../parameters/service-json.md)、[Rds.json](../../parameters/rds-json.md)の値を自動設定します。

XXXでセットアップしたデータベースを選択してください。
表示された指示に従って、プリザンターをセットアップしてください。

=== "SQL Server"

    <div class="steps" markdown>

    1.  インストーラを起動します。以下のコマンドを実行してください。

        ``` text
        pleasanter-setup
        ```

        ??? tip "ネットワークに接続できない場合"
            1.  あらかじめ[ダウンロードセンター](https://pleasanter.org/dlcenter)から最新バージョンのプリザンターをダウンロードし、`C:\web\`に配置してください。`C:\web\`ディレクトリ配下の構成が以下のようになっていることを確認してください。

                ``` text
                C:\web\Pleasanter_1.4.x.x.zip
                ```

            1.  下記のコマンドを実行してください。

                ``` text
                pleasanter-setup -r C:\web\Pleasanter_1.4.11.0.zip
                ```

    1.  プリザンターをインストールするディレクトリを設定します。
        既定では `C:\web\pleasanter` にインストールされます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        Install Directory [Default: C:\web\pleasanter] :
        　
        ```

    1.  サービス名を設定します。
        既定では `Implem.Pleasanter` と設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        ServiceName [Default: Implem.Pleasanter] :
        　
        ```

    1.  使用するデータベースを選択します。
        ++1++ を入力し、++enter++ を押下してください。

        ``` text hl_lines="2"
        DBMS [1: SQL Server, 2: PostgreSQL, 3: MySQL] :
        1
        ```

    1.  データベース接続に利用するポート番号を設定します。
        既定では1433番ポートが設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        Please enter port number[Default: 1433]
        　
        ```

    1.  接続文字列のServerに設定する値を入力します。
        既定では`localhost`が設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        ConnectionString Server [Default: localhost] :
        　
        ```

    1.  SaConnectionStringのUIDに設定する値（ユーザID）を入力します。
        既定では`sa`が設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        SaConnectionString UID [Default: sa] :
        　
        ```

    1.  SaConnectionStringのPWDに設定する値（パスワード）を入力してください。

        ``` text hl_lines="3"
        SaConnectionString PWD :
        Enter your password:
        ********
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  OwnerConnectionStringのPWDに設定する値（パスワード）を入力してください。

        ``` text hl_lines="3"
        OwnerConnectionString PWD :
        Enter your password:
        ************
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  UserConnectionStringのPWDに設定する値（パスワード）を入力します。

        ``` text hl_lines="3"
        UserConnectionString PWD :
        Enter your password:
        ***********
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  「既定の言語」を入力します。
        対応する言語の番号を入力してください。

        ``` text hl_lines="2"
        DefaultLanguage [1: English(Default), 2: Chinese, 3: Japanese, 4: German, 5: Korean, 6: Spanish, 7: Vietnamese] :
        3
        ```

    1.  「既定のタイムゾーン」を入力します。
        対応するタイムゾーンの番号を入力してください。

        ``` text hl_lines="3"
        Set the default time zone.
        TimeZoneDefault [1: UTC(Default), 2: Tokyo Standard Time, 3: Other] :
        2
        ```

        !!! tip "「3: Other」を選択した場合"
            ++3++ を選択した場合は、OSで利用できるタイムゾーンを入力してください。

    1.  サマリ画面が表示されます。入力した値に間違いがないことを確認してください。
        「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. :」に ++y++ を入力し、++enter++ キーを押下して実行してください。

        ``` text hl_lines="28"
        ------ Summary ------
        Install Directory         : C:\web\pleasanter
        DBMS                      : SQLServer
        SaConnectionString PWD    : **********
        OwnerConnectionString PWD : **********
        UserConnectionString PWD  : **********
        Port                      : 1433
        Server                    : localhost
        Service Name              : Implem.Pleasanter
        DefaultLanguage           : ja
        DefaultTimeZone           : Tokyo Standard Time
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
        Shall I install Pleasanter with this content? Please enter `y(yes)' or 'n(no)' . :
        y
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  以下のように表示されたら ++y++ を入力して実行してください。

        ``` text hl_lines="2"
        Type "y" (yes) if the license is correct, otherwise type "n" (no).
        y　
        ```

    1.  インストールするプリザンターのEditionについて確認されます。
        Community Editionの場合は ++y++ と入力し、++enter++ キーを押下してください。

        ``` text hl_lines="3"
        <INFO> Configurator.OutputLicenseInfo: This edition is "Community Edition".
        Type "y" (yes) if the license is correct, otherwise type "n" (no).
        y
        ```

    1.  下記ログが表示されたらセットアップは終了です。

        ``` text
        <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
        <SUCCESS> Starter.Main: All of the processes have been completed.
        Setup is complete.
        ```

    1.  セットアップが終了すると、Webブラウザが起動してEnterprise Editionトライアルの案内ページが表示されます。

        ![セットアップ完了後に Web ブラウザで表示される Enterprise Edition トライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/2f1b98e366bb4477bd5ab45e7d4aa8c0.png)

    </div>

=== ":simple-postgresql: PostgreSQL"

    <div class="steps" markdown>

    1.  インストーラを起動します。以下のコマンドを実行してください。

        ``` text
        pleasanter-setup
        ```

        ??? tip "ネットワークに接続できない場合"
            1.  あらかじめ[ダウンロードセンター](https://pleasanter.org/dlcenter)から最新バージョンのプリザンターをダウンロードし、`C:\web\`に配置してください。`C:\web\`ディレクトリ配下の構成が以下のようになっていることを確認してください。

                ``` text
                C:\web\Pleasanter_1.4.x.x.zip
                ```

            1.  下記のコマンドを実行してください。

                ``` text
                pleasanter-setup -r C:\web\Pleasanter_1.4.11.0.zip
                ```

    1.  プリザンターをインストールするディレクトリを設定します。
        既定では `C:\web\pleasanter` にインストールされます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        Install Directory [Default: C:\web\pleasanter] :
        　
        ```

    1.  サービス名を設定します。
        既定では `Implem.Pleasanter` と設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        ServiceName [Default: Implem.Pleasanter] :
        　
        ```

    1.  使用するデータベースを選択します。
        ++1++ を入力し、++enter++ を押下してください。

        ``` text hl_lines="2"
        DBMS [1: SQL Server, 2: PostgreSQL, 3: MySQL] :
        2
        ```

    1.  データベース接続に利用するポート番号を設定します。
        既定では5432番ポートが設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        Please enter port number[Default: 5432]
        　
        ```

    1.  接続文字列のServerに設定する値を入力します。
        既定では`localhost`が設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        ConnectionString Server [Default: localhost] :
        　
        ```

    1.  SaConnectionStringのUIDに設定する値（ユーザID）を入力します。
        既定では`postgres`が設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        SaConnectionString UID [Default: postgres] :
        　
        ```

    1.  SaConnectionStringのPWDに設定する値（パスワード）を入力してください。

        ``` text hl_lines="3"
        SaConnectionString PWD :
        Enter your password:
        ********
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  OwnerConnectionStringのPWDに設定する値（パスワード）を入力してください。

        ``` text hl_lines="3"
        OwnerConnectionString PWD :
        Enter your password:
        ************
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  UserConnectionStringのPWDに設定する値（パスワード）を入力します。

        ``` text hl_lines="3"
        UserConnectionString PWD :
        Enter your password:
        ***********
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  「既定の言語」を入力します。
        対応する言語の番号を入力してください。

        ``` text hl_lines="2"
        DefaultLanguage [1: English(Default), 2: Chinese, 3: Japanese, 4: German, 5: Korean, 6: Spanish, 7: Vietnamese] :
        3
        ```

    1.  「既定のタイムゾーン」を入力します。
        対応するタイムゾーンの番号を入力してください。

        ``` text hl_lines="3"
        Set the default time zone.
        TimeZoneDefault [1: UTC(Default), 2: Tokyo Standard Time, 3: Other] :
        2
        ```

        !!! tip "「3: Other」を選択した場合"
            ++3++ を選択した場合は、OSで利用できるタイムゾーンを入力してください。

    1.  サマリ画面が表示されます。入力した値に間違いがないことを確認してください。
        「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. :」に ++y++ を入力し、++enter++ キーを押下して実行してください。

        ``` text hl_lines="28"
        ------ Summary ------
        Install Directory         : C:\web\pleasanter
        DBMS                      : PostgreSQL
        SaConnectionString PWD    : **********
        OwnerConnectionString PWD : **********
        UserConnectionString PWD  : **********
        Port                      : 5432
        Server                    : localhost
        Service Name              : Implem.Pleasanter
        DefaultLanguage           : ja
        DefaultTimeZone           : Tokyo Standard Time
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
        Shall I install Pleasanter with this content? Please enter `y(yes)' or 'n(no)' . :
        y
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  以下のように表示されたら ++y++ を入力して実行してください。

        ``` text hl_lines="2"
        Type "y" (yes) if the license is correct, otherwise type "n" (no).
        y　
        ```

    1.  インストールするプリザンターのEditionについて確認されます。
        Community Editionの場合は ++y++ と入力し、++enter++ キーを押下してください。

        ``` text hl_lines="3"
        <INFO> Configurator.OutputLicenseInfo: This edition is "Community Edition".
        Type "y" (yes) if the license is correct, otherwise type "n" (no).
        y
        ```

    1.  下記ログが表示されたらセットアップは終了です。

        ``` text
        <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
        <SUCCESS> Starter.Main: All of the processes have been completed.
        Setup is complete.
        ```

    1.  セットアップが終了すると、Webブラウザが起動してEnterprise Editionトライアルの案内ページが表示されます。

        ![セットアップ完了後に Web ブラウザで表示される Enterprise Edition トライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/2f1b98e366bb4477bd5ab45e7d4aa8c0.png)

    </div>

=== ":simple-mysql: MySQL"

    <div class="steps" markdown>

    1.  インストーラを起動します。以下のコマンドを実行してください。

        ``` text
        pleasanter-setup
        ```

        ??? tip "ネットワークに接続できない場合"
            1.  あらかじめ[ダウンロードセンター](https://pleasanter.org/dlcenter)から最新バージョンのプリザンターをダウンロードし、`C:\web\`に配置してください。`C:\web\`ディレクトリ配下の構成が以下のようになっていることを確認してください。

                ``` text
                C:\web\Pleasanter_1.4.x.x.zip
                ```

            1.  下記のコマンドを実行してください。

                ``` text
                pleasanter-setup -r C:\web\Pleasanter_1.4.11.0.zip
                ```

    1.  プリザンターをインストールするディレクトリを設定します。
        既定では `C:\web\pleasanter` にインストールされます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        Install Directory [Default: C:\web\pleasanter] :
        　
        ```

    1.  サービス名を設定します。
        既定では `Implem.Pleasanter` と設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        ServiceName [Default: Implem.Pleasanter] :
        　
        ```

    1.  使用するデータベースを選択します。
        ++1++ を入力し、++enter++ を押下してください。

        ``` text hl_lines="2"
        DBMS [1: SQL Server, 2: PostgreSQL, 3: MySQL] :
        3
        ```

    1.  データベース接続に利用するポート番号を設定します。
        既定では3306番ポートが設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        Please enter port number[Default: 3306]
        　
        ```

    1.  接続文字列のServerに設定する値を入力します。
        既定では`localhost`が設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        ConnectionString Server [Default: localhost] :
        　
        ```

    1.  SaConnectionStringのUIDに設定する値（ユーザID）を入力します。
        既定では`root`が設定されます。
        ++enter++ キーを押下してください。

        ``` text hl_lines="2"
        SaConnectionString UID [Default: root] :
        　
        ```

    1.  SaConnectionStringのPWDに設定する値（パスワード）を入力してください。

        ``` text hl_lines="3"
        SaConnectionString PWD :
        Enter your password:
        ********
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  OwnerConnectionStringのPWDに設定する値（パスワード）を入力してください。

        ``` text hl_lines="3"
        OwnerConnectionString PWD :
        Enter your password:
        ************
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  UserConnectionStringのPWDに設定する値（パスワード）を入力します。

        ``` text hl_lines="3"
        UserConnectionString PWD :
        Enter your password:
        ***********
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  MySqlConnectingHostに設定する値を入力します。
        既定では「%」に設定されます。
        ++enter++ キーを押下してください。
        バージョン1.4.17.1以前をセットアップする場合は、既定の設定を使用してください。

        ``` text hl_lines="2"
        MySQL Connecting Host [Default: %] :
        　
        ```

        !!! tip "MySQLに対するアクセス制限を行う場合"
            [パラメータ設定：Rds.json](../../parameters/rds-json.md)を参照し、適宜設定してください。

    1.  「既定の言語」を入力します。
        対応する言語の番号を入力してください。

        ``` text hl_lines="2"
        DefaultLanguage [1: English(Default), 2: Chinese, 3: Japanese, 4: German, 5: Korean, 6: Spanish, 7: Vietnamese] :
        3
        ```

    1.  「既定のタイムゾーン」を入力します。
        対応するタイムゾーンの番号を入力してください。

        ``` text hl_lines="3"
        Set the default time zone.
        TimeZoneDefault [1: UTC(Default), 2: Tokyo Standard Time, 3: Other] :
        2
        ```

        !!! tip "「3: Other」を選択した場合"
            ++3++ を選択した場合は、OSで利用できるタイムゾーンを入力してください。

    1.  サマリ画面が表示されます。入力した値に間違いがないことを確認してください。
        「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. :」に ++y++ を入力し、++enter++ キーを押下して実行してください。

        ``` text hl_lines="29"
        ------ Summary ------
        Install Directory         : C:\web\pleasanter
        DBMS                      : MySQL
        SaConnectionString PWD    : **********
        OwnerConnectionString PWD : **********
        UserConnectionString PWD  : **********
        Port                      : 3306
        Server                    : localhost
        Service Name              : Implem.Pleasanter
        MySqlConnectingHost       : %
        DefaultLanguage           : ja
        DefaultTimeZone           : Tokyo Standard Time
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
        Shall I install Pleasanter with this content? Please enter `y(yes)' or 'n(no)' . :
        y
        ```

        !!! warning "パスワードは表示されない"
            入力したパスワードはマスクされ、確認することができません。

    1.  以下のように表示されたら ++y++ を入力して実行してください。

        ``` text hl_lines="2"
        Type "y" (yes) if the license is correct, otherwise type "n" (no).
        y　
        ```

    1.  インストールするプリザンターのEditionについて確認されます。
        Community Editionの場合は ++y++ と入力し、++enter++ キーを押下してください。

        ``` text hl_lines="3"
        <INFO> Configurator.OutputLicenseInfo: This edition is "Community Edition".
        Type "y" (yes) if the license is correct, otherwise type "n" (no).
        y
        ```

    1.  下記ログが表示されたらセットアップは終了です。

        ``` text
        <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
        <SUCCESS> Starter.Main: All of the processes have been completed.
        Setup is complete.
        ```

    1.  セットアップが終了すると、Webブラウザが起動してEnterprise Editionトライアルの案内ページが表示されます。

        ![セットアップ完了後に Web ブラウザで表示される Enterprise Edition トライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/2f1b98e366bb4477bd5ab45e7d4aa8c0.png)

    </div>

## :four: IISのセットアップ

「サーバー マネージャー」を使い、IISを設定します。

<div class="steps" markdown>

1.  「サーバー マネージャー」の「ツール」メニューを開き、「インターネット インフォメーション サービス (IIS) マネージャー」を起動します。
1.  左ペインの「アプリケーションプール」-「DefaultAppPool」を選択し、右ペインの「基本設定」をクリックします。

    ![IISマネージャーの「アプリケーションプール」画面。「DefaultAppPool」と「基本設定」がある](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/b9cf77af523842d3b44849a971102d2a.png)

1.  「.Net CLR バージョン」を、「マネージド コードなし」に変更し、「OK」ボタンをクリックします。

    ![「アプリケーションプールの編集」ダイアログ。「.Net CLR バージョン」を「マネージド コードなし」にする](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/28023d94c0cb462d8b179d25f1e6b289.png)

1.  左ペインの「サイト」-「Default Web Site」を選択し、右ペインの「詳細設定」をクリックします。

    ![IISマネージャーで「Default Web Site」を選び、右ペインの「詳細設定」を開くところ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/562f44f19999462a9f7a998b5c3cf551.png)

1.  「物理パス」に「C:\web\pleasanter\Implem.Pleasanter」と入力し、「OK」ボタンをクリックします。

    ![「詳細設定」ダイアログ。「物理パス」にプリザンターの配置先を入力する](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/e0e5d4a4eb8743a3a7596dbcbb492c4b.png)

1.  左ペインの「サイト」-「Default Web Site」を選択し、右ペインの「再起動」をクリックして、IISを再起動します。

    ![IISマネージャーで「Default Web Site」を選び、右ペインの「再起動」をクリックするところ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/a22c0a41993443b8b0abe955b3ab01bd.png)

1.  再起動後、右ペインの「*.80(http)参照」をクリックし、プリザンターを起動します。

    ![IISマネージャーの右ペイン。「*.80(http)参照」の項目がある](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/dc336addd7294f90b94e0810752fac5d.png)

</div>

## :five: プリザンターの動作確認

初期ユーザでプリザンターへログインし、初期ユーザのパスワードを変更します。

<div class="steps" markdown>

1.  Webブラウザーが起動し、プリザンターのログイン画面が表示されます。
    以下の情報を入力し、「ログイン」ボタンをクリックしてください。

    | ラベル         |入力情報       |
    | :------------- |:------------- |
    | ログインID     | Administrator |
    | 初期パスワード | pleasanter    |

    ![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/2eedf079c23240618539fe8f3fa41910.png)

1.  ログイン後にユーザ「Administrator」のパスワード変更を求められます。
    任意のパスワードを2度入力し、「変更」ボタンをクリックしてください。

    ![初回ログイン後に表示される、Administrator のパスワード変更画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/4c5d1cf2c148489d87f763a2bf83aebe.png)

</div>

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.9.0 以降|MySQLに対応|
|1.4.10.0 以降|MySQLのアクセス制御機能によりOwner、Userの接続が拒否される場合がある問題を解消[^1]|
|1.4.18.0 以降|MySQLのDBへの接続元ホストにlocalhost（DBと同一のサーバ）以外を指定する機能を追加|
|1.5.0.0 以降|.NET 10、Windows Server 2025、SQL Server 2025、PostgreSQL 18に対応|

[^1]: 併せて注意事項に「WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）」へのリンクを追加
