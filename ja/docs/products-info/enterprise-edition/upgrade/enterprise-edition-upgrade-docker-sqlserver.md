---
title: Community EditionからEnterprise Editionへのアップグレード手順（Docker利用／DBにSQL Serverを利用）
category: 初回導入手順
order: '0'
status: ''
parts: ''
urlstring: enterprise-edition-upgrade-docker-sqlserver
translationKey: enterprise-edition-upgrade-docker-sqlserver
shortname: Community EditionからEnterprise Editionへのアップグレード手順（Docker利用／DBにSQL Serverを利用）
created: 2026-07-12
updated: 2026-07-17
---

## Docker版プリザンターについて

以下では、Docker Hubで公開されているプリザンターの公式Dockerイメージを利用します。

[implem/pleasanter - Docker Image | Docker Hub](https://hub.docker.com/r/implem/pleasanter)

## 概要

データベースにSQL Serverを指定して、Community Editionから[Enterprise Edition](enterprise-edition-upgrade-docker.md)へアップグレードする手順について説明します。

## 注意事項

1. Community Editionから[Enterprise Edition](../index.md)にアップグレードすると以下の動作となります。
   1. 「ライセンス」が商用ライセンスになります。ライセンスは「共通機能：バージョン」画面で確認できます。
   1. 「[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)」、「[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)」、「[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)」、「[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)」、「[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)」、「[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)」の利用数を拡張することができます。
   1. 契約した「年間サポートサービスプラン」に応じてユーザ登録数の上限が設定され、上限を超えてユーザを登録することができません。
   1. [Pleasanter Extensions](../../pleasanter-extensions/index.md)（[Pleasanter Site Visualizer](../../pleasanter-extensions/pleasanter-site-visualizer/index.md)、[Pleasanter Code Assist](../../pleasanter-extensions/pleasanter-code-assist/index.md)、[Operations Tools](../../pleasanter-extensions/operations-tools/index.md)、[Development Tools](../../pleasanter-extensions/development-tools/index.md)）が利用可能になります。
1. 本ページの手順は、プリザンターをすぐに試したいユーザのために、SQL Serverコンテナをプリザンターと同一のDocker構成に含めた複数コンテナ構成を採用しています。この構成は**本番運用を想定したものではありません**。
1. 本番運用では、データベースコンテナが性能上のボトルネックになります。**別ホスト上のデータベース**とすることを強く推奨します。

## 前提事項

1. 本手順は、以下のマニュアルの手順通り実施し、パラメータファイルを変更して起動できることを前提としています。  
「Dockerイメージを使用しDBにSQL Serverを指定して起動する」

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
    |   +-- 📄Rds.json
    |   +-- 📄Service.json
    |
    +-- 📁license                  ← 新規作成
    |    +-- 📄Implem.License.dll  ← ここに配置
    |
    |-- 📄.env
    |-- 📄compose.yaml
    +-- 📁CodeDefiner
    |    +-- 📄Dockerfile
    +-- 📁Pleasanter
    |    +-- 📄Dockerfile
    +-- 📁SQL Server
         +-- 📄Dockerfile
   ```

</div>

### 3. Dockerfileの修正

CodeDefinerフォルダ、Pleasanterフォルダ内のDockerfileを、それぞれ以下のとおり修正してください。

##### CodeDefiner/Dockerfile

```dockerfile
FROM implem/pleasanter:codedefiner

COPY app_data_parameters/ /app/Implem.Pleasanter/App_Data/Parameters/
COPY Implem.License.dll .
ENTRYPOINT [ "dotnet", "Implem.CodeDefiner.dll" ]
```

##### Pleasanter/Dockerfile

```dockerfile
ARG VERSION=latest
FROM implem/pleasanter:${VERSION}

COPY app_data_parameters/ App_Data/Parameters/
COPY Implem.License.dll .
ENTRYPOINT [ "dotnet", "Implem.Pleasanter.dll" ]
```

### 4. イメージのビルド

Enterprise Editionにアップグレードしたイメージをビルドします。以下のコマンドを実行してください。

```bash
docker compose build
```

### 5. コンテナの再作成と再起動

Enterprise Editionにアップグレードしたコンテナを作成し、起動します。以下のコマンドを実行してください。

```bash
docker compose up -d pleasanter
```

### 6. 動作確認

<div class="steps" markdown>

1. ブラウザで以下のURLを開いてください。

       ```text
       http://localhost:8881
       ```

1. プリザンターにログインしてください。
1. 「共通機能：バージョン」画面を開きます。ナビゲーションメニューの「ヘルプ」をクリックし、「バージョン」をクリックしてください。
1. 以下の3点を確認してください。

    1. ライセンスが「商用ライセンス」となっていること
    1. ライセンス期限が正しいこと
    1. 使用者が正しいこと

</div>

## 項目拡張作業

Community Editionでは「[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)」、「[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)」、「[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)」、「[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)」、「[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)」、「[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)」の各項種別毎に26個、計156項目が利用できますが、[Enterprise Edition](../index.md)では項目を拡張することができます。

| DB         | Enterprise Editionで利用できる項目の上限 |
| :--------- | :--------------------------------------- |
| PostgreSQL | 6つの項目種別の合計で最大900個まで       |
| MySQL[^1]  | 6つの項目種別の合計で最大256個まで       |

[^1]: MySQLはver1.4.9.0以降のプリザンターで使用できます。

項目拡張を行う場合は「Docker利用時の項目拡張の手順」に沿って作業を行ってください。

## 関連情報

-   [implem/pleasanter - Docker Image | Docker Hub](https://hub.docker.com/r/implem/pleasanter)
-   [Community EditionからEnterprise Editionへのアップグレード手順(Docker利用)](enterprise-edition-upgrade-docker.md)
