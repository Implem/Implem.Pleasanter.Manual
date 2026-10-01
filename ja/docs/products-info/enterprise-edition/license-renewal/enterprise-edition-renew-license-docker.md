---
title: ライセンス更新手順(Docker利用)
category: ライセンス更新手順
order: '201'
status: ''
parts: ''
urlstring: enterprise-edition-renew-license-docker
translationKey: enterprise-edition-renew-license-docker
shortname: Enterprise Edition,ライセンス更新
created: 2025-03-19
updated: 2026-07-17
---

## Docker版プリザンターについて

Docker Hubで公開されているプリザンターの公式Dockerイメージを利用する手順です。

implem/pleasanter - Docker Image | Docker Hub  
https://hub.docker.com/r/implem/pleasanter

## 概要

年間サポートサービスの契約更新を行いEnterprise Editionの利用期限を延長された場合は、本手順にそってライセンスファイルを更新してください。

## 制限事項

1. ライセンスファイルの期限が過ぎると以下の動作となります。
   1. ライセンスがAGPL（GNU AFFERO GENERAL PUBLIC LICENSE）に戻ります。
   1. 項目拡張していた場合、拡張した項目が非表示となります。ただしデータベース上のデータは保存済みのままです。
   1. ユーザ登録数の上限が解除されます。
   1. Pleasanter Extensions（Development Tools、Operations Tools、Pleasanter Code Assist）が利用不可となります。  

## 前提条件

1. 本手順はプリザンターをEnterprise Editionにアップグレードしていることを前提とします。

## 操作手順

### 1. ライセンスファイルの格納

<div class="steps" markdown>

1. コンテナを停止します。以下コマンドを実行します。

    ```bash
    docker compose stop
    ```

2. ライセンスパックに含まれる「Implem.License.dll」を .envファイル および compose.yamlファイル と同じフォルダに上書きコピーします。

</div>

### 2. アップグレードの確認

<div class="steps" markdown>

1. 以下コマンドを実行し、コンテナイメージを再ビルドします。

    ```bash
    docker compose build
    ```

2. 以下コマンドを実行し、Enterprise Editionにアップグレードしたコンテナの再作成と再起動を行います。

    ```bash
    docker compose up -d pleasanter
    ```

3. ブラウザでアクセスします。  
    <http://localhost:50001>

4. プリザンターにログインし、ナビゲーションメニューの「ヘルプ」－「バージョン」より以下を確認してください。

    -   ライセンスが「商用ライセンス」となっていること
    -   ライセンス期限が正しいこと（2月末までのライセンスの場合、3/1と表示されます）
    -   使用者が正しいこと

</div>

### 3. 項目拡張作業

Community Editionでは[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)、[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)、[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)、[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)の各項種別毎に26個、計156項目が利用できますが、Enterprise Editionでは項目を拡張することができます。

| DB         | Enterprise Editionで利用できる項目の上限 |
| ---------- | ---------------------------------------- |
| PostgreSQL | 6つの項目種別の合計で最大900個まで       |
| MySQL[^1]  | 6つの項目種別の合計で最大256個まで       |

[^1]: MySQLはver1.4.9.0以降のプリザンターで使用できます。

ライセンス更新と合わせて項目拡張の増減を行う場合は[Docker利用時の項目拡張](../columns-expansion/enterprise-edition-columns-expansion-docker.md)の手順に沿って作業を行ってください。

## 関連情報

-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [項目拡張手順（Docker利用）](../columns-expansion/enterprise-edition-columns-expansion-docker.md)
