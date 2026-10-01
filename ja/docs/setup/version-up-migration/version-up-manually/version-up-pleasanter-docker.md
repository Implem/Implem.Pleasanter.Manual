---
title: Dockerイメージのプリザンターをバージョンアップする
category: バージョンアップ
order: '3000'
status: ''
parts: ''
urlstring: version-up-pleasanter-docker
translationKey: version-up-pleasanter-docker
shortname: バージョンアップ手順,Dockerのバージョンアップ手順
created: 2024-12-03
updated: 2026-07-17
---

## 概要

以下手順でセットアップした公式Dockerイメージのプリザンターをバージョンアップする手順です。

-   [Dockerで起動する](../../installation/running-with-docker/getting-started-pleasanter-docker.md)
-   [Dockerイメージを使用しパラメータを既定値から変更して起動する](../../installation/running-with-docker/change-parameters-at-docker-image.md)
-   [Dockerイメージを使用しDBにMySQLを指定して起動する](../../installation/running-with-docker/setup-by-docker-image-and-mysql.md)

Docker Hubで公開されている公式Dockerイメージについては以下を参照してください。

-   [implem/pleasanter - Docker Image | Docker Hub](https://hub.docker.com/r/implem/pleasanter)

## 注意事項

1.  ver1.4.5以前で実施する場合はCodeDefinerのコマンドが変更されているため、以下ページを参照してください。  
[ver1.4.6以降で初回インストール時のCodeDefinerの手順について](../../installation/prerequisites/codedefiner-changed-steps.md)

## 操作手順

### 1. プリザンターの停止

以下コマンドを実行し、プリザンターのコンテナを停止します。

``` bash
docker compose stop
```

### 2. app_data_parametersフォルダ等の追加

今回のバージョンアップで新しく`app_data_parameters`フォルダを作成し、「[Dockerイメージを使用しパラメータを既定値から変更して起動する](../../installation/running-with-docker/change-parameters-at-docker-image.md)」方式に切り替える場合、以下手順を実施します。

-   PostgreSQLのみ必要となる場合がある手順です。
-   MySQL利用時はapp_data_parametersフォルダが必須です。現行フォルダの使用を続けてください。

??? note "手順を確認する"

    1.  フォルダ構成を以下の内容に修正します。

        ``` text
        .
        |-- compose.yaml
        |-- .env
        |
        +-- app_data_parameters
        |   +-- 拡張機能用フォルダ
        |   |   +-- 拡張機能用ファイル
        |   |  
        |   +-- パラメータファイル
        |
        +-- CodeDefiner
        |   +-- Dockerfile
        |
        +---Pleasanter
            +-- Dockerfile
        ```

    1.  /CodeDefiner/Dockerfileを以下の内容で作成します。

        ``` text title="/CodeDefiner/Dockerfile"
        FROM implem/pleasanter:codedefiner

        COPY app_data_parameters/ /app/Implem.Pleasanter/App_Data/Parameters/
        ENTRYPOINT [ "dotnet", "Implem.CodeDefiner.dll" ]
        ```

    1.  Pleasanter/Dockerfileを以下の内容で作成します。

        ``` text title="Pleasanter/Dockerfile"
        ARG VERSION=latest
        FROM implem/pleasanter:${VERSION}

        COPY app_data_parameters/ App_Data/Parameters/
        ENTRYPOINT [ "dotnet", "Implem.Pleasanter.dll" ]
        ```

    1.  .envファイルの内容を修正します。

        -   環境変数「PLEASANTER_VER」に指定する{{Version}}（次期バージョン）は、Docker Hubで公開されているプリザンターのバージョンを指定してください（例：latest，1.4.10.1　等）。
        -   {{Version}}以外は現行の.envファイルと同じ内容を設定してください。

        ``` text title=".env"
        POSTGRES_USER={{Sa User}}
        POSTGRES_PASSWORD={{Sa Password}}
        POSTGRES_DB={{System DB}}
        POSTGRES_HOST_AUTH_METHOD=scram-sha-256
        POSTGRES_INITDB_ARGS="--auth-host=scram-sha-256 --encoding=UTF-8"
        PLEASANTER_VER={{Version}}
        Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString='Server=db;Database={{System DB}};UID={{Sa User}};PWD={{Sa password}}'
        Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString='Server=db;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD={{Owner password}}'
        Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString='Server=db;Database=#ServiceName#;UID=#ServiceName#_User;PWD={{User password}}'
        ```

    1.  compose.yamlファイルの内容を修正します。

        ``` yaml title="compose.yaml"
        services:
        db:
            container_name: postgres
            image: postgres:17
            environment:
            - POSTGRES_USER
            - POSTGRES_PASSWORD
            - POSTGRES_DB
            - POSTGRES_HOST_AUTH_METHOD
            - POSTGRES_INITDB_ARGS
            volumes:
            - type: volume
                source: pg_data
                target: /var/lib/postgresql/data
        pleasanter:
            build:
            context: .
            dockerfile: ./Pleasanter/Dockerfile
            args:
                - VERSION=${PLEASANTER_VER}
            container_name: pleasanter_${PLEASANTER_VER}
            depends_on:
            - db
            ports:
            - '50001:8080'
            environment:
            Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
            Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
            Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
        codedefiner:
            build:
            context: .
            dockerfile: ./CodeDefiner/Dockerfile
            container_name: codedefiner
            depends_on:
            - db
            environment:
            Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
            Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
            Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
        volumes:
        pg_data:
            name: ${COMPOSE_PROJECT_NAME:-default}_pg_data_volume
        ```

### 3. パラメータファイルの更新

現行バージョンの運用中、app_data_parametersフォルダにパラメータファイルを格納していた場合は、以下手順を実施します。

??? note "手順を確認する"

    #### 1. パラメータファイルのバックアップ

    1.  現行パラメータファイルをバックアップします。このバックアップは手順3.3.1.で使用します。パラメータファイルはDockerイメージをマニュアル通りにセットアップした場合、app_data_parametersフォルダ内のjsonファイルとなります。
    1.  **拡張機能を利用していない場合は本手順は不要です。** 拡張機能で設定した現行パラメータファイルをバックアップします。このバックアップは手順3.4.1.で使用します。拡張機能で設定したファイルはDockerイメージをマニュアル通りにセットアップした場合、app_data_parametersフォルダ配下にある以下サブフォルダ内のファイルとなります。

        | サブフォルダ名          | 拡張機能名                                                                                                       | 備考                                                         |
        | :---------------------- | :--------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------- |
        | CustomDefinitions       | [拡張項目](../../../developers-guide/extended-features/extended-column.md)                                       | 組織、グループ、ユーザに項目を追加した際に生成されるフォルダ |
        | ExtendedFields          | [拡張フィールド](../../../developers-guide/extended-features/extended-fields.md)                                 |                                                              |
        | ExtendedHtmls           | [拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md) |                                                              |
        | ExtendedNavigationMenus | [拡張ナビゲーションメニュー](../../../developers-guide/extended-features/extended-navigationmenus.md)            |                                                              |
        | ExtendedScripts         | [拡張スクリプト](../../../developers-guide/extended-features/extended-script.md)                                 |                                                              |
        | ExtendedServerScripts   | [拡張サーバスクリプト](../../../developers-guide/extended-features/extended-server-script.md)                    |                                                              |
        | ExtendedSqls            | [拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)                                     |                                                              |
        | ExtendedStyles          | [拡張スタイル](../../../developers-guide/extended-features/extended-style.md)                                    |                                                              |

    #### 2. アプリケーションの準備

    1.  [ダウンロードセンター](https://pleasanter.org/dlcenter)から、次期バージョンのプリザンターをダウンロードします。
    1.  ダウンロードしたzipファイルを解凍します。
    1.  解凍したフォルダの「\pleasanter\Implem.Pleasanter\App_Data\Parameters」およびサブフォルダに格納されているファイルを、次期バージョンのパラメータファイルとします。

    #### 3. パラメータ再設定

    1.  手順3.2.3.で準備した次期バージョンのパラメータファイルに対して、現行で設定済みの内容を反映します。[WinMerge](https://winmergejp.bitbucket.io/)などのファイル比較・マージツールを利用して次期バージョンのパラメータファイルと手順3.1.1.で取得した現行バックアップファイルのパラメータファイルを比較しながら次期バージョンのパラメータファイルを修正します。<br>**Service.jsonが配置されている場合は、TimeZoneDefaultが正しい値か確認してください。TimeZoneDefaultにはPleasanterをインストールするサーバのOSで有効なタイムゾーンを設定してください。（Windowsなら"Tokyo Standard Time"など、Linuxなら"Asia/Tokyo"など）**
        [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)
    1.  app_data_parametersフォルダ内のパラメータファイルを、次期バージョンのパラメータファイルに差し替えます。

    #### 4. 拡張機能の再設定

    **拡張機能を利用していない場合は本手順は不要です。**

    1.  手順3.2.3.で準備した次期バージョンの拡張機能用パラメータファイルに対して、現行で設定済みの内容を反映します。[WinMerge](https://winmergejp.bitbucket.io/)などのファイル比較・マージツールを利用して次期バージョンの拡張機能用パラメータファイルと手順3.1.2.で取得した現行バックアップファイルの拡張機能用パラメータファイルを比較しながら次期バージョンの拡張機能用パラメータファイルを修正します。
    1.  app_data_parametersフォルダ配下のサブフォルダ内の拡張機能用パラメータファイルを、次期バージョンの拡張機能用パラメータファイルに差し替えます。

## 4. パラメータファイルの新規追加

app_data_parametersフォルダに新しいパラメータファイルを追加し、既定値から変更する場合は、以下手順を実施します。

??? note "手順を確認する"

    1.  [ダウンロードセンター](https://pleasanter.org/dlcenter)から、次期バージョンのプリザンターをダウンロードします。
    1.  zipファイルを解凍します。
    1.  解凍したフォルダの「\pleasanter\Implem.Pleasanter\App_Data\Parameters」に格納されている、対象のパラメータファイルをapp_data_parametersフォルダ配下にコピーします。
    1.  コピーしたパラメータファイルを編集します。

## 5. ファイルに記載のバージョンを変更

1.  プリザンターのバージョンを記述したファイルを確認します。

    === "[Dockerで起動する](../../installation/running-with-docker/getting-started-pleasanter-docker.md)方式"

        ``` yaml title="compose.yaml"
        image: implem/pleasanter:{{Version}}
        ```

    === "[Dockerイメージを使用しパラメータを既定値から変更して起動する](../../installation/running-with-docker/change-parameters-at-docker-image.md)方式"

        ``` text title=".env"
        PLEASANTER_VER={{Version}}
        ```

1.  {{Version}}が「latest」の場合は変更不要です。「6.次期バージョンのコンテナイメージを作成」以降を実施します。
    {{Version}}で直接バージョンを指定している場合は、次期バージョンとして「Docker Hubで公開されているバージョン番号」または「latest」に変更した後、「6.次期バージョンのコンテナイメージを作成」以降を実施します。

## 6. 次期バージョンのコンテナイメージを作成

ビルドすると共に、オプションに`--pull`を指定してコンテナイメージを更新します。

``` bash
docker compose build --pull
```

## 7. CodeDefinerの実行

以下コマンドを実行します。

Dockerイメージを使用する場合に限り、バージョンアップ時のコマンドに`/l`、`/z`の引数設定が必要です。

``` bash
docker compose run --rm codedefiner _rds /l "<言語>" /z "<タイムゾーン>"
```

| 引数 | 設定例     | 説明                                                 |
| :--- | :--------- | :--------------------------------------------------- |
| /l   | ja         | Service.jsonのDefaultLanguageの値を書き換えます [^1] |
| /z   | Asia/Tokyo | Service.jsonのTimeZoneDefaultの値を書き換えます [^1] |

[^1]:
    言語、タイムゾーンは以下マニュアルページを参照ください。
    [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

日本語環境でご利用する場合は以下コマンドとなります。

``` bash
docker compose run --rm codedefiner _rds /l "ja" /z "Asia/Tokyo"
```

途中で 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら ++y++ を入力してください。

コンソールログに以下のようにバージョンが出力されます。ここで表示されるバージョンは常に「Docker Hubで公開されている最新のプリザンターのバージョン」となります。このコンソールログ表示の仕様は、ファイルの{{Version}}に最新よりも前のバージョンを指定した場合も同様ですが、データベースは{{Version}}に準拠した内容で作成されますので、プリザンターの動作上の問題はありません。

``` text
<INFO> Starter.Main: Implem.CodeDefiner 1.4.10.1
```

## 8. プリザンターの起動確認

1.  以下コマンドを実行します。
    停止して残っていた現行バージョンのプリザンターのコンテナが、次期バージョンのコンテナとして再作成され、起動します。

    ``` bash
    docker compose up -d pleasanter
    ```

1.  ブラウザでアクセスし、ログインします。

    [http://localhost:50001](http://localhost:50001)

1.  ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。
