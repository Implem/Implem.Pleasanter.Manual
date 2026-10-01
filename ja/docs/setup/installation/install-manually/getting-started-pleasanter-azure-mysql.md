---
title: プリザンターをAzure App Serviceにサーバレス構成でインストールする（Azure Database for MySQL利用）
category: プリザンターのインストール
order: '800'
status: ''
parts: ''
urlstring: getting-started-pleasanter-azure-mysql
translationKey: getting-started-pleasanter-azure-mysql
shortname: プリザンターのインストール,App Serviceにインストール
created: 2025-05-21
updated: 2026-04-20
---

## 概要

Microsoft AzureのApp ServiceとMicrosoft Azure Database for MySQLを利用し、サーバレス構成でプリザンターの動作環境を構築するための手順を示します。

| 対象               | 環境・バージョン                                        |
| ------------------ | :------------------------------------------------------ |
| Web                | Microsoft Azure App Service                             |
| DB                 | Microsoft Azure Database for MySQL<br>（MySQL 8.4 LTS） |
| ランタイムスタック | .NET 10                                                 |
| Pleasanter         | 1.5.0.0以降                                             |

## 注意事項

1. 引数を指定せずにCodeDefinerを実行した場合、言語：英語、タイムゾーン：UTCでセットアップされます。必要に応じて言語とタイムゾーンを指定してください。

## 前提条件

1. Azure Portalへのログインが可能であること
1. Microsoft Azure App Service（Windows/.NET 10）を1インスタンス準備できていること
1. Microsoft Azure Database for MySQLを1インスタンス準備できていること
1. Microsoft Azure Database for MySQLのサーバ名、管理ユーザ名、管理ユーザパスワードを準備できていること
1. Microsoft Azure Database for MySQLのファイアウォール設定でApp ServiceおよびローカルPCからの接続が許可されていること

## 手順

構築手順は以下の通りです。

1. 事前準備
1..NETの設定
1. Azure Database for MySQLのサーバー パラメータ変更
1. プリザンターのダウンロードおよびパラメータ設定
1. プリザンターの配置
1. CodeDefinerの実行
1. プリザンターの起動確認

## 1. .NET の設定

1. [Azure Portal](https://portal.azure.com/)に接続します。
1. App Service を開きます。
    ![Azure Portal で App Service を開いたところ](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/1e9a46eb0bd24007bc14ae1111d42c7c.png)
1. 作成済みの App Service インスタンスを選択します。
1. 「構成」メニューの「全般設定」を開き、下図の通り設定します。
   ![App Service の「構成」の「全般設定」の画面](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/b1521673e01f4055a29fbc31fdec576c.png)
   ![App Service の「全般設定」の画面。設定項目の続き](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/bcfe86d9950b49a2ba5baf02bc26a08d.png)

    | 番号 | 項目              | 設定内容                                    |
    | :--: | :---------------- | :------------------------------------------ |
    |  1   | 構成 (プレビュー) | クリックして選択します                      |
    |  2   | 全般設定          | クリックして選択します                      |
    |  3   | プラットフォーム  | 64bit                                       |
    |  4   | FTPの状態         | 無効                                        |
    |  5   | Always On         | オン（※常時接続と表示されることがあります） |
    |  6   | スタック設定      | クリックして選択します                      |
    |  7   | スタック          | .NET                                        |
    |  8   | .NETのバージョン  | .NET 10 (LTS)                               |

## 2. Azure Database for MySQLのサーバー パラメータ変更

1.  [Azure Portal](https://portal.azure.com/)に接続します。
1.  Azure Database for MySQLを開きます。  
    ![Azure Portal で Azure Database for MySQL を開いたところ](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/33d2d2adfa964ba99b9115766efebd55.png)
1.  作成済みの Microsoft Azure Database for MySQL インスタンスを選択します。
1.  「設定」メニューの「サーバパラメータ」を開きます。
1.  「すべて」タブをクリックします。
1.  「sql_generate_invisible_primary_key」を検索します。
1.  「sql_generate_invisible_primary_key」を「OFF」に設定します。  
    ![Azure Database for MySQL のサーバパラメータの画面。sql_generate_invisible_primary_key を OFF にする](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/ea15da303b0d427094422b6d8ea0711d.png)
1.  上部の「保存」ボタンをクリックします。

## 3. プリザンターのダウンロードおよびパラメータ設定

1.  [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。
1.  ダウンロードしたzipファイルを解凍します。
1.  パラメータファイルを設定します。
    1.  データベースへの接続情報を設定します。  
        「pleasanter\Implem.Pleasanter\App_Data\Parameters\Rds.json」を開き、パラメータを下記の通りに設定し、保存します。

        | パラメータ名                | 値    | 説明                                                                                                                  |
        | :-------------------------- | :---- | :-------------------------------------------------------------------------------------------------------------------- |
        | Dbms                        | MySQL | リレーショナル・データベースにMicrosoft Azure Database for MySQLを使用。                                              |
        | Provider                    | Local | リレーショナル・データベースにMicrosoft Azure Database for MySQLを使用。                                              |
        | SaConnectionString          | null  | データベースインスタンスにSA権限で接続するための接続文字列。<br>nullを設定する（手順3.3.2参照）。                     |
        | OwnerConnectionString       | null  | Pleasanterのデータベースにdbowner権限で接続するための接続文字列。<br>nullを設定する（手順3.3.3参照）。                |
        | UserConnectionString        | null  | Pleasanterのデータベースにdbreader権限、dbwriter権限で接続するための接続文字列。<br>nullを設定する（手順3.3.4参照）。 |
        | SqlCommandTimeOut           | 0     | SQLコマンドタイムアウト時間を無期限にする。                                                                           |
        | MinimumTime                 | 3     | データベースが識別可能な最小時間単位をミリ秒で指定。本パラメータは変更しないでください。                              |
        | DeadlockRetryCount          | 4     | デッドロック発生時の最大再試行回数。                                                                                  |
        | DeadlockRetryInterval       | 1000  | デッドロック発生時に再試行を行うまでの間隔。                                                                          |
        | DisableIndexChangeDetection | true  | バージョンアップ時にデータベースのインデックスの差異を検出しない。                                                    |
        | SysLogsSchemaVersion        | 2     | [システムログの拡張機能](../../../managers-guide/system-log-administration/syslog-extension.md)を利用する。                                                                                |
        | MySqlConnectingHost         | %     | App Serviceのホストから接続を許可するためワイルドカードを指定。                                                       |

    1.  [Rds.json](../../parameters/rds-json.md)のパラメータSaConnectionStringにnullを設定し、環境変数Implem.Pleasanter_Rds_MySQL_SaConnectionStringに以下の値を設定します。

        ```text
        {ServerName}.mysql.database.azure.com;Port=3306;Database=mysql;UID={UserName};PWD={Password}
        ```

        { } の部分は、以下の説明を参考に、適切な文字列へ書き替えてください。

        | No. | 書き替える場所 | 説明                                                       |
        | :-: | :------------- | :--------------------------------------------------------- |
        |  1  | {ServerName}   | Microsoft Azure Database for MySQLのサーバ名。             |
        |  2  | {UserName}     | Microsoft Azure Database for MySQLの管理ユーザ名。         |
        |  3  | {Password}     | Microsoft Azure Database for MySQLの管理ユーザパスワード。 |

    1.  [Rds.json](../../parameters/rds-json.md)のパラメータOwnerConnectionStringにnullを設定し、環境変数Implem.Pleasanter_Rds_MySQL_OwnerConnectionStringに以下の値を設定します。

        ```text
        Server={ServerName}.mysql.database.azure.com;Port=3306;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD={SetAdminsPWD}
        ```

        { } の部分は、以下の説明を参考に、適切な文字列へ書き替えてください。

        | 書き替える場所 | 説明                                                             |
        | :------------- | :--------------------------------------------------------------- |
        | {ServerName}   | 上記No.1で設定したMicrosoft Azure Database for MySQLのサーバ名。 |
        | {SetAdminsPWD} | CodeDefinerで設定する任意のユーザのパスワード。                  |

        なお、#ServiceName#は[Service.json](../../parameters/service-json.md)のパラメータNameの値を表すプレースホルダで、CodeDefinerで作成する任意のユーザ名を意味します。

    1.  [Rds.json](../../parameters/rds-json.md)のパラメータUserConnectionStringにnullを設定し、環境変数Implem.Pleasanter_Rds_MySQL_UserConnectionStringに以下の値を設定します。

        ```text
        Server={ServerName}.mysql.database.azure.com;Port=3306;Database=#ServiceName#;UID=#ServiceName#_User;PWD={SetUsersPWD}
        ```

        { } の部分は、以下の説明を参考に、適切な文字列へ書き替えてください。

        | 書き替える場所 | 説明                                                             |
        | :------------- | :--------------------------------------------------------------- |
        | {ServerName}   | 上記No.1で設定したMicrosoft Azure Database for MySQLのサーバ名。 |
        | {SetUsersPWD}  | CodeDefinerで設定する任意のユーザのパスワード。                  |

        なお、#ServiceName#は[Service.json](../../parameters/service-json.md)のパラメータNameの値を表すプレースホルダで、CodeDefinerで作成する任意のユーザ名を意味します。

## 4. プリザンターの配置

1.  App Serviceにてインスタンスを停止してください。
1.  [Kudu](https://docs.microsoft.com/ja-jp/azure/app-service/resources-kudu#access-kudu-for-your-app) にアクセスしてください。
    1. App Serviceの左側のメニューの「開発ツール」から「高度なツール」をクリックしてください。  
     ![App Service の左メニューの「開発ツール」。「高度なツール」がある](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/406ee90486774cddb8ec698543dc4fb0.png)
    2. 「移動」のリンクをクリックしてください。  
      ![高度なツール（Kudu）の画面。「移動」のリンクがある](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/a0fa0b2d1664446084c93478aa12a6bf.png)
    3. Kuduのヘッダメニューから「Debug console」→「CMD」をクリックしてください。  
      ![Kudu のヘッダメニュー。「Debug console」から「CMD」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/8376f1283cc44e03acf78972e2195bac.png)
    4. ディレクトリ一覧から「site」をクリックし、プロンプトが"C:\home\site"になったことを確認してください。（ユーザによってはD:\home\siteなどとなる場合があります。適宜読み替えてください。）  
      ![Kudu の Debug console。ディレクトリ一覧から「site」を選んだ状態](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/980d266c0d1b43f98b6cf9e4185c6fdd.png)

1.  「2. プリザンターのダウンロードおよびパラメータ設定」で準備したプリザンターファイルをApp Serviceへアップロードします。
    1.  「pleasanter」フォルダに移動してください。
    2.  「Implem.Pleasanter」フォルダを「wwwroot」にリネームしてください。
    3.  wwwrootフォルダをzip形式で圧縮してください。（wwwroot.zipとなります。）
    4.  「Implem.CodeDefiner」フォルダを[CodeDefiner](../../codedefiner/codedefiner-command.md)にリネームします。
    5.  CodeDefinerフォルダをzip形式で圧縮してください。（CodeDefiner.zipとなります。）
    6.  wwwroot.zipとCodeDefiner.zipをKuduのSizeをターゲットにドラッグアンドドロップし、展開されて格納されたことを確認します。  
        ![Kudu の Debug console。wwwroot.zip と CodeDefiner.zip が展開されて格納された状態](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/9276162cc96b4cc4adea3818252925a4.png)

## 5. CodeDefiner の実行

1.  Kuduのディレクトリ一覧からCodeDefinerを選択し、 プロンプトがC:\home\site\CodeDefinerとなることを確認します。
2.  以下のコマンドを実行して、CodeDefinerを実行します。以下のコマンドは、初回インストール時にのみ実行します。
    ```
    dotnet Implem.CodeDefiner.dll _rds /p C:\home\site\wwwroot /l "<言語>" /z "<タイムゾーン>"
    ```

    | 引数 | 設定例              | 説明                                            |
    | :--- | :------------------ | :---------------------------------------------- |
    | /l   | ja                  | Service.jsonのDefaultLanguageの値を書き換えます |
    | /z   | Tokyo Standard Time | Service.jsonのTimeZoneDefaultの値を書き換えます |

    /lに指定できる言語、/zに指定できるタイムゾーンの詳細については、以下のマニュアルを参照してください。  
    [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

    ▼日本語環境で利用する場合の実行例

    ```
    dotnet Implem.CodeDefiner.dll _rds /p C:\home\site\wwwroot /l "ja" /z "Tokyo Standard Time"
    ```

## 6. プリザンターの起動確認

1.  App Serviceにてインスタンスを起動します。
1.  ブラウザでプリザンターのログイン画面を開き、「ログインID: Administrator」、「初期パスワード: pleasanter」を入力し、「ログイン」ボタンをクリックします。  
    ![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/5477647dc121413190827affdc7fa1ff.png)
1.  ログイン後に「Administrator」ユーザーのパスワード変更を求められるので、任意のパスワードを入力し、「変更」ボタンをクリックします。  
    ![初回ログイン後に表示される、Administrator のパスワード変更画面](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/d57262564d8e49568553a84b273d3797.png)
