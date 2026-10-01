---
title: プリザンターのDBデータを定期的にバックアップしたい（SQL Server）
category: FAQ：バックアップ、リストア
order: '500'
status: ''
parts: ''
urlstring: faq-backup-schedule
translationKey: faq-backup-schedule
shortname: バックアップ
created: 2019-04-15
updated: 2024-12-19
---

## 回答

SQL Server Integration Service Manager（SSIS）で[バックアップ](faq-backup-and-restore.md)の定期実行設定を行ってください。

SQL Server Expressをご利用の場合は「[プリザンターのデータベース(SQL Server)をバックアップする](../../setup/additional/db-server/backup-sql-server.md)」を参照ください。

---

## 概要

データベースにSQL Serverを利用する場合、データベースのバックアップを定期実行するにはSQL Server Integration Service Manager（SSIS）で設定することができます。

SQL Server Expressをご利用の場合はSSISは利用できないので、[プリザンターのデータベース(SQL Server)をバックアップする](../../setup/additional/db-server/backup-sql-server.md)」を参照してください。

## 操作手順

### 1. SQL Server Integration Service Manager（SSIS）のインストール

!!! info
    既にインストールされている場合はこちらの手順を飛ばしてください。

1.  SQL Server 2017のメディアよりインストーラを起動し、[インストール]-[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加]を選択します。

    ![SQL Server インストーラの［インストール］画面。新規スタンドアロンインストールの項目が並ぶ](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/bb0a7d91c31f453eaea92291b873329d.png)

1.  SQL Server セットアップウィザードに従い、インストールを進めます。
1.  [インストールの種類]にて、「既存の SQL Server 2017 インスタンスに機能を追加する(A)」を選択し、対象のインスタンスを選択したら「次へ(N)」を選択します。

    ![セットアップウィザードの［インストールの種類］画面。既存インスタンスへの機能追加を選ぶ](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/9231abf702b2463499671339d47a3eeb.png)

1.  [機能の選択]にて、[機能(F)]より「Integration Services」にチェックを入れ、「次へ(N)」を選択します。

    ![セットアップウィザードの［機能の選択］画面。Integration Services にチェックが入っている](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/20e88f282e3f45dfa14e6272fac6195c.png)

1.  SQL Server セットアップウィザードに従い、インストールを進めます。
1.  インストール完了後、[SQL Server 2022 構成マネージャー]を起動し、SSISのサービスを開始します。

    ![SQL Server 構成マネージャーで SSIS のサービスを開始したところ](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/f2297219c3114ddba26ac4f1fc2f3c71.png)

1.  SQL Server エージェントが実行中でない場合、右クリック「プロパティ」を選択し、プロパティダイアログの[ログオン]タブより「開始」をクリックしてください。また、[サービス]タブより[開始モード]を「自動」に変更してください。

### 2. メンテナンスプランの設定

1.  SQL Server Management Studioより、対象のSQL Serverから[管理]フォルダを展開し、[メンテナンス プラン] フォルダーを右クリック「メンテナンス プラン ウィザード(W)」を選択します。

    ![SQL Server Management Studio の［メンテナンス プラン］フォルダーの右クリックメニュー](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/82d839df2b6b42cea40346e13a2964bf.png)

    !!! info
        メンテナンスウィザードの詳細については、下記のMicrosoft社のドキュメントを確認してください。

        [メンテナンス プラン ウィザードの使用 - SQL Server | Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/relational-databases/maintenance-plans/use-the-maintenance-plan-wizard?view=sql-server-2017)

1.  メンテナンス プラン ウィザードに従い、設定を進めます。
1.  [プランのプロパティを選択]にて、以下の設定を行います。

    -   名前：メンテナンスプランの名称を任意に設定
    -   「プラン全体で単一のスケジュールを使用するか、スケジュールを使用しない」を選択
    -   スケジュール：「変更」を選択

    ![メンテナンス プラン ウィザードの［プランのプロパティを選択］画面](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/61e42292b75a4cdcb04edb7fcb4f3670.png)

1.  [新しいジョブスケジュール]にて、以下の設定を行い「OK」を選択します。

    -   頻度：任意の頻度を設定（今回設定のジョブが実行される頻度の設定）
    -   1日のうちの頻度：頻度の到来時に1回だけ実行するか、一定の間隔で実行し続けるかを設定
    -   実行時間：任意の実行時間を設定（今回設定のジョブスケジュールを開始する日付を設定）

    ![［新しいジョブスケジュール］の画面。頻度と実行時間を設定する](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/4a15d073adee42198c0ab1b4e17cf89a.png)

1.  スケジュールを確認し、「次へ(N)」を選択します。

    ![ウィザードのスケジュール確認画面。設定したスケジュールが表示されている](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/6b5bf11b116e41e788d89496c8d58f2b.png)

1.  [メンテナンス タスクの選択]にて、「データベースのバックアップ（完全）」、「メンテナンス クリーンアップ タスク」にチェックを付け、「次へ(N)」を選択します。

    ![［メンテナンス タスクの選択］画面。バックアップとクリーンアップにチェックが入っている](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/b8d9fc58d303448a9565521d576b8748.png)

1.  [メンテナンス タスクの順序を選択]にて、「データベースのバックアップ（完全）」→「メンテナンス クリーンアップ タスク」の順番に設定して「次へ(N)」を選択します。

    ![［メンテナンス タスクの順序を選択］画面。バックアップ、クリーンアップの順に並ぶ](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/9ae220db3e1f44bcb6eaa54ad8215dd4.png)

1.  [データベースのバックアップ（完全）タスクの定義]にて、[全般]タブで以下の設定を行います。

    -   データベース：バックアップを行うデータベース（プリザンターで使用しているデータベース）を設定
    -   バックアップ コンポーネント：データベース全体をバックアップするには「データベース(E)」を選択

    ![［データベースのバックアップ（完全）タスクの定義］の［全般］タブ](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/ef27d4bf563245d7800ff19b72eabe3d.png)

1.  [バックアップ先]タブにて、以下の設定を行い「次へ(N)」を選択します。

    -   すべてのデータベースにバックアップファイルを作成する：「フォルダー(L)」にバックアップファイルを作成するフォルダーを指定
    -   バックアップ ファイルの拡張子(O)："bak"を指定

    ![同タスク定義の［バックアップ先］タブ。出力フォルダーと拡張子を指定する](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/3718a218ec9941f186d4a61669959213.png)

1.  [メンテナンス クリーンアップ タスクの定義]にて、以下の設定を行い「次へ(N)」を選択します。

    -   次の種類のファイルを削除：「バックアップ ファイル(K)」を選択
    -   ファイルの場所：「フォルダーを検索し、拡張子に基づいてファイルを削除する(O)」を選択
        -   「フォルダー(D):」にバックアップファイルを削除するフォルダーを指定  
        -   「ファイル拡張子(I):」に"bak"を指定
    -   ファイルの経過時間：「タスク実行時にファイルの経過期間に基づいてファイルを削除する(T)」にチェック  
        -   「次の期間経過したファイルを削除(G):」に「8日」を指定（プリザンター マニュアルでご案内しているDbBackup.vbsと同様の削除日程）

    ![［メンテナンス クリーンアップ タスクの定義］画面。削除対象と経過日数を指定する](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/24c15edbd9864de0ada9fe4a1eeeeb96.png)

1.  メンテナンス プラン ウィザードに従い、メンテナンスプランの設定を完了します。

## 関連情報

-   [FAQ：プリザンターのDBデータをバックアップする方法とリストアする方法を知りたい](faq-backup-and-restore.md)
-   [プリザンターのデータベース(SQL Server)をバックアップする](../../setup/additional/db-server/backup-sql-server.md)
