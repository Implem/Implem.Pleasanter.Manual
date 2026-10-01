---
title: Enterprise Editionアップグレード済みプリザンターのバージョンアップ手順(Docker利用)
category: バージョンアップ手順
order: '501'
status: ''
parts: ''
urlstring: enterprise-edition-version-up-docker
translationKey: enterprise-edition-version-up-docker
shortname: ''
created: 2025-05-08
updated: 2026-07-17
---

## Docker版プリザンターについて

Docker Hubで公開されているプリザンターの公式Dockerイメージを利用する手順です。

-   [implem/pleasanter - Docker Image | Docker Hub](https://hub.docker.com/r/implem/pleasanter)

## 概要

Enterprise Editionご利用中の環境においてプリザンターをバージョンアップする際の手順について説明します。特に項目拡張を行っている場合は必ず本手順を確認してください。

## 注意事項

1.  バージョンアップ作業前にデータベースバックアップを必ず取得してください。  

    -   [FAQ：PostgreSQL データベース バックアップ・リストア手順(Docker利用)](../../../FAQ/backup-restore/faq-postgresql-backup-restore-docker.md)  
    -   [FAQ：MySQL データベース バックアップ・リストア手順(Docker利用)](../../../FAQ/backup-restore/faq-mysql-backup-restore-docker.md)

1.  ライセンスファイルは必ず現在契約中のものを使用してください。特に項目拡張を行っている場合、期限切れのライセンスファイルを用いてCodeDefinerを実行すると拡張した項目が削除され、入力済みデータを参照できなくなります。  

## 前提条件

1.  本手順はプリザンターをEnterprise Editionにアップグレードしていることを前提とします。

## 操作手順

### 1. バージョンアップ実行（CodeDefinerの実行前まで）

<div class="steps" markdown>

1.  「[Dockerイメージのプリザンターをバージョンアップする](../../../setup/version-up-migration/version-up-manually/version-up-pleasanter-docker.md)」手順の以下項番を参照し、バージョンアップ作業を実施してください。「2.app_data_parametersフォルダ等の追加」の実施は不要です。

    -   1\. プリザンターの停止
    -   3\. パラメータファイルの更新
    -   4\. パラメータファイルの新規追加
    -   5\. ファイルに記載のバージョンを変更
    -   6\. 次期バージョンのコンテナイメージを作成

</div>

### 2. バージョンアップ実行（CodeDefinerの実行）

<div class="steps" markdown>

1.  「Dockerイメージのプリザンターをバージョンアップする」手順の項番7「CodeDefinerの実行」を実施します。

    #### 次期バージョンが1.4.8以降の場合

    「CodeDefinerの実行」にて項目拡張の使用数削減が起こる場合、エラーメッセージ「\<ERROR\> Configurator.CheckColumnsShrinkage: The columns will be shrinked.」が表示されて終了し、CodeDefinerは実行されません。エラーとなった場合は下図のように削減する項目が表示されますので、パラメータファイルおよびライセンスが正しく適用されているか再度確認ください。

    ![項目の削減が発生してCodeDefinerがエラー終了したログ](https://pleasanter.org/files/images/ja/products-info/enterprise-edition/version-up/assets/1a435488422c42ddb2e5d8b980753720.png)

    項目の削減を許容する場合は、「CodeDefinerの実行」で実行するコマンドに引数「/f」を指定して、実行してください。

    ``` text
    dotnet Implem.CodeDefiner.dll _rds /f
    ```

</div>

### 3. プリザンターの起動

<div class="steps" markdown>

1.  以下コマンドを実行します。  
    停止して残っていた現行バージョンのプリザンターのコンテナが、次期バージョンのコンテナとして再作成され、起動します。

    ``` text
    docker compose up -d pleasanter
    ```

1.  ブラウザでアクセスし、ログインします。

    [http://localhost:50001](http://localhost:50001)

</div>

### 4. バージョンアップの確認

<div class="steps" markdown>

1.  プリザンターにログインし、ナビゲーションメニューの「ヘルプ」－「バージョン」より以下を確認してください。

    -   ライセンスが「商用ライセンス」となっていること
    -   ライセンス期限が正しいこと（2月末までのライセンスの場合、3/1と表示されます）
    -   使用者が正しいこと
    -   バージョンが正しいこと

1.  項目拡張済みの場合は以下を確認してください。

    -   任意のテーブルを開き、ナビゲーションメニューの[管理]-[テーブルの管理]より[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブにて、選択肢一覧のリストに拡張した項目（分類001、数値001等）が表示されること
    -   拡張した項目を設定したテーブルの編集画面を開き、項目がすべて表示していること

</div>

## 関連情報

-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
