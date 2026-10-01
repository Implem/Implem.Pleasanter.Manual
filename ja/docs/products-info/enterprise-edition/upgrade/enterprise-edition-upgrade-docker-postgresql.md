---
title: Community EditionからEnterprise Editionへのアップグレード手順（Docker利用／DBにPostgreSQLを利用）
category: 初回導入手順
order: '102'
status: ''
parts: ''
urlstring: enterprise-edition-upgrade-docker-postgresql
translationKey: enterprise-edition-upgrade-docker-postgresql
shortname: Community EditionからEnterprise Editionへのアップグレード手順（Docker利用／DBにPostgreSQLを利用）
created: 2026-07-12
updated: 2026-07-17
---

## Docker版プリザンターについて

以下では、Docker Hubで公開されているプリザンターの公式Dockerイメージを利用します。

[implem/pleasanter - Docker Image | Docker Hub](https://hub.docker.com/r/implem/pleasanter)

## 概要

データベースにPostgreSQLを指定して、Community Editionから[Enterprise Edition](enterprise-edition-upgrade-docker.md)へアップグレードする手順について説明します。

## 注意事項

1. Community Editionから[Enterprise Edition](../index.md)にアップグレードすると以下の動作となります。
   1. 「ライセンス」が商用ライセンスになります。ライセンスは「共通機能：バージョン」画面で確認できます。
   1. 「[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)」、「[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)」、「[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)」、「[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)」、「[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)」、「[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)」の利用数を拡張することができます。
   1. 契約した「年間サポートサービスプラン」に応じてユーザ登録数の上限が設定され、上限を超えてユーザを登録することができません。
   1. [Pleasanter Extensions](../../pleasanter-extensions/index.md)（[Pleasanter Site Visualizer](../../pleasanter-extensions/pleasanter-site-visualizer/index.md)、[Pleasanter Code Assist](../../pleasanter-extensions/pleasanter-code-assist/index.md)、[Operations Tools](../../pleasanter-extensions/operations-tools/index.md)、[Development Tools](../../pleasanter-extensions/development-tools/index.md)）が利用可能になります。
1. 本ページの手順は、プリザンターをすぐに試したいユーザのために、PostgreSQLコンテナをプリザンターと同一のDocker構成に含めた複数コンテナ構成を採用しています。この構成は**本番運用を想定したものではありません**。
1. 本番運用では、データベースコンテナが性能上のボトルネックになります。**別ホスト上のデータベース**とすることを強く推奨します。

## 前提条件

1. 本手順は、以下のマニュアルの手順通り実施し、パラメータファイルを変更して起動できることを前提としています。  
「Dockerイメージを使用しパラメータを既定値から変更して起動する」

## 操作手順

### 1. プリザンターのバージョンアップ

アップグレードの前に、以下の手順に従ってバージョンアップを実施してください。

「Dockerイメージのプリザンターをバージョンアップする」

### 2. ライセンスファイルの格納

<div class="steps" markdown>

1. コンテナを停止します。以下のコマンドを実行してください。

       ```bash
       docker compose stop
       ```

1. app_data_parametersフォルダと同じ階層にlicenseフォルダを新規作成してください。
1. ライセンスパックに含まれる「Implem.License.dll」をlicenseフォルダ内へコピーしてください。

       フォルダ構成は以下の通りです。

       ```text
       📁pleasanter
        +-- 📁app_data_parameters
        |   +-- 📁拡張機能用フォルダ
        |   |   +-- 📄拡張機能用ファイル
        |   |
        |   +-- 📄パラメータファイル
        |
        +-- 📁license                    ←新規作成
        |    +-- 📄Implem.License.dll    ←ここに配置
        |
        |-- 📄.env
        |-- 📄compose.yaml
       ```

1. PleasanterとCodeDefinerからImplem.License.dllを参照できるように、compose.yamlを以下のように編集します。  

    以下はcompose.yamlの抜粋です。

    ##### compose.yaml（抜粋）

    ```yaml
    pleasanter:
        : 中略
    volumes:
      - pleasanter_params:/app/App_Data/Parameters
      - ./license/Implem.License.dll:/app/Implem.License.dll:ro  #←追記
        : 中略
    codedefiner:
        : 中略
    volumes:
      - codedefiner_params:/app/Implem.Pleasanter/App_Data/Parameters
      - ./license/Implem.License.dll:/app/Implem.CodeDefiner/Implem.License.dll:ro  #←追記
    ```

    | サービス    | 配置先                                     |
    | :---------- | :----------------------------------------- |
    | pleasanter  | /app/Implem.License.dll                    |
    | codedefiner | /app/Implem.CodeDefiner/Implem.License.dll |

    ##### compose.yaml（全体）

    ```yaml
    services:
      db:
        container_name: postgres
        image: postgres:${POSTGRES_VERSION}
        environment:
          - POSTGRES_USER
          - POSTGRES_PASSWORD
          - POSTGRES_DB
          - POSTGRES_HOST_AUTH_METHOD
          - POSTGRES_INITDB_ARGS
        volumes:
          - type: volume
            source: pg_data
            target: ${POSTGRES_VOLUMES_TARGET}
        networks:
          - backend
        healthcheck:
          test:
            [
              "CMD-SHELL",
              "pg_isready -U $${POSTGRES_USER:-postgres} -d $${POSTGRES_DB:-postgres} || exit 1",
            ]
          interval: 10s
          timeout: 5s
          retries: 5
          start_period: 30s
        restart: unless-stopped
      param-init:
        container_name: param-init
        image: implem/pleasanter:${PLEASANTER_VERSION}
        volumes:
          - ./app_data_parameters:/tmp/app_data_parameters:ro
          - pleasanter_params:/app/App_Data/Parameters
        entrypoint:
          - sh
          - -c
          - cp -rf /tmp/app_data_parameters/. /app/App_Data/Parameters/ && echo "Parameters copied"
        restart: "no"
        network_mode: none
      param-init-codedefiner:
        container_name: param-init-codedefiner
        image: implem/pleasanter:codedefiner
        volumes:
          - ./app_data_parameters:/tmp/app_data_parameters:ro
          - codedefiner_params:/app/Implem.Pleasanter/App_Data/Parameters
        entrypoint:
          - sh
          - -c
          - cp -rf /tmp/app_data_parameters/. /app/Implem.Pleasanter/App_Data/Parameters/ && echo "Parameters copied"
        restart: "no"
        network_mode: none
      pleasanter:
        container_name: pleasanter
        image: implem/pleasanter:${PLEASANTER_VERSION}
        restart: unless-stopped
        depends_on:
          db:
            condition: service_healthy
          param-init:
            condition: service_completed_successfully
        ports:
          - '50001:8080'
        environment:
          Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
          Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
          Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
        volumes:
          - pleasanter_params:/app/App_Data/Parameters
          - ./license/Implem.License.dll:/app/Implem.License.dll:ro
        networks:
          - backend
      codedefiner:
        container_name: codedefiner
        image: implem/pleasanter:codedefiner
        depends_on:
          db:
            condition: service_healthy
          param-init-codedefiner:
            condition: service_completed_successfully
        environment:
          Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
          Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
          Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
        volumes:
          - codedefiner_params:/app/Implem.Pleasanter/App_Data/Parameters
          - ./license/Implem.License.dll:/app/Implem.CodeDefiner/Implem.License.dll:ro
        networks:
          - backend
    networks:
      backend:
    volumes:
      pg_data:
        name: ${COMPOSE_PROJECT_NAME:-default}_pg_data_volume
      pleasanter_params:
        name: ${COMPOSE_PROJECT_NAME:-default}_pleasanter_params_volume
      codedefiner_params:
        name: ${COMPOSE_PROJECT_NAME:-default}_codedefiner_params_volume
    ```

</div>

### 3. コンテナの再作成と再起動

<div class="steps" markdown>

1. Enterprise Editionにアップグレードしたコンテナの再作成と再起動を行います。以下のコマンドを実行してください。

       ```bash
       docker compose up -d pleasanter
       ```

</div>

### 4. アップグレードの確認

<div class="steps" markdown>

1. ブラウザで以下のURLを開いてください。

       ```text
       http://localhost:50001
       ```

1. プリザンターにログインしてください。
1. 「共通機能：バージョン」画面を開きます。ナビゲーションメニューの「ヘルプ」をクリックし、「バージョン」をクリックしてください。
1. 以下の3点を確認してください。

    1. ライセンスが「商用ライセンス」となっていること
    1. ライセンス期限が正しいこと
    1. 使用者が正しいこと

</div>

## 項目拡張作業

Community Editionでは「[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)」、「[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)」、「[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)」、「[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)」、「[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)」、「[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)」の各項種別毎に26個、計156項目が利用できますが、Enterprise Editionでは項目を拡張することができます。

| DB         | Enterprise Editionで利用できる項目の上限 |
| ---------- | ---------------------------------------- |
| PostgreSQL | 6つの項目種別の合計で最大900個まで       |
| SQL Server | 6つの項目種別の合計で最大900個まで       |
| MySQL[^1]  | 6つの項目種別の合計で最大256個まで       |

[^1]: プリザンター1.4.9.0以降で使用できます。

項目拡張を行う場合は「[Docker利用時の項目拡張](../columns-expansion/enterprise-edition-columns-expansion-docker.md)」の手順に沿って作業を行ってください。

## 関連情報

-   [implem/pleasanter - Docker Image | Docker Hub](https://hub.docker.com/r/implem/pleasanter)
-   [Community EditionからEnterprise Editionへのアップグレード手順(Docker利用)](enterprise-edition-upgrade-docker.md)
