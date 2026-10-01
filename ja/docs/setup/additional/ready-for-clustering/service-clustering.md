---
title: バックグラウンドサービスを複数インスタンス構成に対応させる
category: 追加設定：クラスタ化への備え
order: '100'
status: ''
parts: ''
urlstring: service-clustering
translationKey: service-clustering
shortname: バックグラウンドサービスを複数インスタンス構成に対応させる
created: 2025-10-30
updated: 2026-01-13
---

## 概要

プリザンターのバックグラウンドサービスを複数インスタンス構成に対応させる機能です。

たとえば、ロードバランサとデータベースとの間に、プリザンターが稼働する2台のサーバ（複数インスタンス）を設置する構成を考えます。各インスタンスでリマインダー機能を有効化すると、次のような事象が発生します。

### 通常設定の場合

![通常設定の構成図。2台のインスタンスそれぞれでリマインダーが実行される](https://pleasanter.org/files/images/ja/setup/additional/ready-for-clustering/assets/0e8339f9240f441894faae7f936967b5.png)

各インスタンスでリマインダーが実行され、不要なメール送信が実行されてしまいます。

### 各インスタンスでバックグラウンドサービスを複数インスタンス構成に対応させた場合

![複数インスタンス構成に対応させた構成図。1台でのみリマインダーが実行される](https://pleasanter.org/files/images/ja/setup/additional/ready-for-clustering/assets/e22a1d4bb7a843c3a8a23c5064cd3f0c.png)

1つのインスタンスでのみリマインダーが実行され、不要なメール送信は実行されません。

### 複数インスタンス構成に対応するバックグラウンドサービス

複数インスタンス構成に対応するバックグラウンドサービスは、以下の通りです。

1. 本設定により、複数インスタンス環境下の1台のサーバのみで実行されるサービス  

    |サービス名|パラメータファイル|パラメータ名|
    |:--|:--|:--|
    |バックグラウンドサーバスクリプト|[Script.json](../../parameters/script-json.md)|BackgroundServerScript|
    |リマインダー|[BackgroundService.json](../../parameters/background-service-json.md)|Reminder|
    |LDAP同期|[BackgroundService.json](../../parameters/background-service-json.md)|SyncByLdap|
    |システムログ削除|[BackgroundService.json](../../parameters/background-service-json.md)|DeleteSysLogs|
    |ごみ箱内レコード削除|[BackgroundService.json](../../parameters/background-service-json.md)|DeleteTrashBox|
    |ごみ箱の内レコードに関連する未使用の権限やリンク情報を削除|[BackgroundService.json](../../parameters/background-service-json.md)|DeleteUnusedRecord|
    |MCPログ削除|[BackgroundService.json](../../parameters/background-service-json.md)|DeleteMcpLogs|

1. 本設定完了後も、複数インスタンス環境下の全サーバで実行されるサービス  

    |サービス名|パラメータファイル|パラメータ名|
    |:--|:--|:--|
    |テンポラリファイル削除|[BackgroundService.json](../../parameters/background-service-json.md)|DeleteTemporaryFiles|

## 注意事項

1. <span class="pl-attention">複数インスタンス構成での運用にあたっては、安定した動作を確保するため、セッション維持機能を有効にした構成（セッションアフィニティ / スティッキーセッション ）を推奨します。</span>
1. ロードバランサ（LB）のバックエンドにプリザンターを導入したサーバが複数台ある環境を想定した説明です。

## 前提条件

1. 開発環境など、TLSサーバ証明書が設定されていないSQL Serverをデータベースとして使用する場合、SaConnectionStringなどの接続情報にTrustServerCertificate=True;を追加してください。  
   【例】Implem.Pleasanter_Rds_SQLServer_SaConnectionStringの場合
   ```
   Server=(local);Database=master;UID=sa;PWD=<設定したパスワード>;Connection Timeout=30;TrustServerCertificate=True;
   ```
1. 複数インスタンス構成での運用にあたっては、[添付ファイルのアップロード・登録に関する設定](clustering-attachment-item-settings.md)も実施してください。

## 設定方法

以下の手順を実行することで、プリザンターのバックグラウンドサービスを複数インスタンス構成に対応させます。なお、本手順の実行後には、「QRTZ_」で始まるテーブルが11個作成されます。

パラメータの設定は、複数インスタンス構成下の全てAPサーバで実施してください。

1. 設定ファイル[Quartz.json](../../parameters/quartz-json.md)のパラメータ「Enabled」の値をtrueに設定してください。
   ```
   "Clustering": {
           "Enabled": true,
         : (途中省略)
   }
   ```
2. [CodeDefiner](../../codedefiner/codedefiner-command.md)を実行してください。

## 対応バージョン

|対応バージョン|説明|
|:--|:--|
|バージョン1.4.22.0|機能追加|

## 関連情報

-   [パラメータ設定：Script.json](../../parameters/script-json.md)
-   [パラメータ設定：BackgroundService.json](../../parameters/background-service-json.md)
-   [追加設定：クラスタ化への備え：添付ファイルのアップロード・登録に関する設定](clustering-attachment-item-settings.md)
-   [パラメータ設定：Quartz.json](../../parameters/quartz-json.md)
-   [CodeDefinerのコマンド一覧](../../codedefiner/codedefiner-command.md)