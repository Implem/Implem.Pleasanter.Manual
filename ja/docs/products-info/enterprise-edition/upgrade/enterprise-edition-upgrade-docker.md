---
title: Community EditionからEnterprise Editionへのアップグレード手順(Docker利用)
category: 初回導入手順
order: '101'
status: ''
parts: ''
urlstring: enterprise-edition-upgrade-docker
translationKey: enterprise-edition-upgrade-docker
shortname: Enterprise Edition,アップグレード
created: 2025-03-19
updated: 2026-07-17
---

## Docker版プリザンターについて

Docker Hubで公開されているプリザンターの公式Dockerイメージを利用する手順です。

implem/pleasanter - Docker Image | Docker Hub  
https://hub.docker.com/r/implem/pleasanter

## 概要

プリザンターをCommunity EditionからEnterprise Editionへアップグレードする手順について説明します。

## 注意事項

Enterprise Editionにアップグレードすると以下の動作となります。

1.  ライセンスが商用ライセンスになります。ナビゲーションメニューの「ヘルプ」－「バージョン」にて確認できます。
1.  分類項目、数値項目などの各項目の利用数を拡張することができます。
1.  契約した年間サポートサービスプランに応じてユーザ登録数の上限が設定され、上限を超えてユーザを登録することができません。
1.  Pleasanter Extensions（Development Tools、Operations Tools、Pleasanter Code Assist）が利用可能になります。  
    なお、データベースにMySQLを使用する場合はPleasanter Extensionsの利用に制限がございます。詳細は「[データベースによる制限事項](../../limitations-database.md)」を参照してください。

## 操作手順

### 1. プリザンターの準備

既にCommunity Editionとしてご利用中のプリザンターをEnterprise Editionにアップグレードする場合は「1-1. プリザンターのバージョンアップ」を実施してください。プリザンターの新規インストールと合わせてEnterprise Editionにアップグレードする場合は「1-2. プリザンターのインストール」を実施してください。

#### 1-1. プリザンターのバージョンアップ

アップグレードの前に弊社オンラインマニュアルの手順にそってバージョンアップを実施してください。
「Dockerイメージのプリザンターをバージョンアップする」

**既存で「app_data_parameters」フォルダを運用していない場合**
「[Dockerイメージのプリザンターをバージョンアップする](../../../setup/version-up-migration/version-up-manually/version-up-pleasanter-docker.md)」 手順でバージョンアップを行う際、**必ず「2.app_data_parametersフォルダ等の追加」**を参照し、以下に示すDocker関連の資源を追加・修正してください。

-   app_data_parametersフォルダ の追加（格納するフォルダ・ファイルがない場合であっても、空の app_data_parametersフォルダ を追加してください）
-   CodeDefinerフォルダ および CodeDefiner/Dockerfileファイル の作成
-   Pleasanterフォルダ および Pleasanter/Dockerfileファイル の作成
-   .envファイル の修正
-   compose.yamlファイル の修正

#### 1-2. プリザンターのインストール

弊社オンラインマニュアルの手順にそってプリザンターをインストールし、ログイン画面が表示することを確認してください。

-   PostgreSQLを使用する場合

    「Dockerイメージを使用しパラメータを既定値から変更して起動する」

    ※app_data_parametersフォルダ に格納するフォルダ・ファイルがない場合であっても、空の app_data_parametersフォルダ を配備してください。

-   MySQLを使用する場合

    「Dockerイメージを使用しDBにMySQLを指定して起動する」

### 2. ライセンスファイルの格納

<div class="steps" markdown>

1.  コンテナを停止します。以下コマンドを実行します。

    ```bash
    docker compose stop
    ```

1.  ライセンスパックに含まれる「Implem.License.dll」を .envファイル および compose.yamlファイル と同じフォルダにコピーします。

</div>

### 3. Dockerfileの修正

<div class="steps" markdown>

1.  CodeDefiner/Dockerfileを以下の内容で修正します。

    ```text
    FROM implem/pleasanter:codedefiner

    COPY app_data_parameters/ /app/Implem.Pleasanter/App_Data/Parameters/
    COPY Implem.License.dll .
    ENTRYPOINT [ "dotnet", "Implem.CodeDefiner.dll" ]
    ```

1.  Pleasanter/Dockerfileを以下の内容で修正します。

    ```text
    ARG VERSION=latest
    FROM implem/pleasanter:${VERSION}

    COPY app_data_parameters/ App_Data/Parameters/
    COPY Implem.License.dll .
    ENTRYPOINT [ "dotnet", "Implem.Pleasanter.dll" ]
    ```

</div>

### 4. アップグレードの確認

<div class="steps" markdown>

1.  以下コマンドを実行し、コンテナイメージを再ビルドします。

    ```bash
    docker compose build
    ```

1.  以下コマンドを実行し、Enterprise Editionにアップグレードしたコンテナの再作成と再起動を行います。

    ```bash
    docker compose up -d pleasanter
    ```

1.  ブラウザでアクセスします。  
    <http://localhost:50001>

1.  プリザンターにログインし、ナビゲーションメニューの「ヘルプ」－「バージョン」より以下を確認してください。

    -   ライセンスが「商用ライセンス」となっていること
    -   ライセンス期限が正しいこと（2月末までのライセンスの場合、3/1と表示されます）
    -   使用者が正しいこと

</div>

### 5. 項目拡張作業

Community Editionでは[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)、[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)、[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)、[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)の各項種別毎に26個、計156項目が利用できますが、Enterprise Editionでは項目を拡張することができます。

| DB          | Enterprise Editionで利用できる項目の上限 |
| :---------- | :--------------------------------------- |
| PostgreSQL  | 6つの項目種別の合計で最大900個まで       |
| MySQL[^1]   | 6つの項目種別の合計で最大256個まで       |

[^1]: MySQLはver1.4.9.0以降のプリザンターで使用できます。

項目拡張を行う場合は[Docker利用時の項目拡張](../columns-expansion/enterprise-edition-columns-expansion-docker.md)の手順に沿って作業を行ってください。

## 関連情報

-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [項目拡張手順（Docker利用）](../columns-expansion/enterprise-edition-columns-expansion-docker.md)
