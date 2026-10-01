---
title: Quartz.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: quartz-json
translationKey: quartz-json
shortname: Quartz.json
created: 2025-10-27
updated: 2026-01-13
---

## 注意事項

1. パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。
1. 下記のパラメータEnabledをtrueに設定する前に、以下のマニュアルを確認してください。

    -   [バックグラウンドサービスを複数インスタンス構成に対応させる](../additional/ready-for-clustering/service-clustering.md)  
    -   [添付ファイルのアップロード・登録に関する設定](../additional/ready-for-clustering/clustering-attachment-item-settings.md)  
    -   [ヘルスチェック機能](../additional/ops-management/enable-health-check.md)

## 制限事項

1. パラメータEnabledをtrueにした後は、必ず[CodeDefiner](../codedefiner/codedefiner-command.md)を実行してください。
1. 開発環境など、TLSサーバ証明書が設定されていないSQL Serverをデータベースとして使用する場合は、SaConnectionStringなどの接続情報にTrustServerCertificate=True;を追加してください。

## 設定値

本ファイルで設定可能なパラメータは下記の通りです。

各パラメータの詳細は、下記ページ（外部サイトへ移動します）を参考にしてください。
[Quartz.NET Configuration Reference](https://www.quartz-scheduler.net/documentation/quartz-3.x/configuration/reference.html)

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Clustering|省略|以下の7つのパラメータを格納するJSONオブジェクトです。|
|Enabled|false|バックグラウンドサービスの排他制御機能を有効化・無効化する設定です。複数のインスタンスでジョブ管理を協調する場合にtrueを設定します。|
|SchedulerName|"PleasanterScheduler"|スケジューラの識別名です。複数インスタンス構成時は全インスタンスで同じ名前を指定する必要があります。quartz.scheduler.instanceNameに設定されます。|
|InstanceId|"AUTO"|スケジューラのインスタンスIDです。通常"AUTO"で自動割り当てされます。quartz.scheduler.instanceIdに設定されます。|
|CheckinInterval|15000|ノードが定期的に状態を確認する間隔（ミリ秒）です。quartz.jobStore.clusterCheckinIntervalに設定されます。|
|MaxMisfireThreshold|60000|ミスファイア（遅延実行）判定のしきい値（ミリ秒）です。quartz.jobStore.clusterCheckinMisfireThresholdに設定されます。|
|TablePrefix|"QRTZ_"|Quartzが使用するDBテーブルの接頭辞です。quartz.jobStore.tablePrefixに設定されます。|
|Serializer|"json"|ジョブデータのシリアライザ種別です。|
|ThreadPool|省略|以下の2つのパラメータを格納するJSONオブジェクトです。quartz.serializer.typeに設定されます。|
|MaxConcurrency|10|スレッドプールの最大同時実行数です。ジョブの並列実行数を制御します。quartz.threadPool.maxConcurrencyに設定されます。|
ThreadPriority|"Normal"|スレッドの優先度です。quartz.threadPool.threadPriorityに設定されます。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.22.0|機能追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [追加設定：クラスタ化への備え：バックグラウンドサービスを複数インスタンス構成に対応させる](../additional/ready-for-clustering/service-clustering.md)
-   [追加設定：クラスタ化への備え：添付ファイルのアップロード・登録に関する設定](../additional/ready-for-clustering/clustering-attachment-item-settings.md)
-   [プリザンターのヘルスチェック機能を有効化する](../additional/ops-management/enable-health-check.md)
-   [CodeDefinerのコマンド一覧](../codedefiner/codedefiner-command.md)
-   [Quartz.NET Configuration Reference](https://www.quartz-scheduler.net/documentation/quartz-3.x/configuration/reference.html)