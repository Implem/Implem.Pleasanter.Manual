---
title: キューイング：マルチノード構成での注意事項
category: その他
order: '0'
status: ''
parts: ''
urlstring: manage-multi-tenant-cueuing-clustering
shortname: マルチテナント管理機能：キューイング：マルチノード構成での注意事項
created: 2026-09-04
updated: 2026-09-08
---

## 概要

「[マルチテナント管理機能](manage-multi-tenant.md)」の使用時に、マルチノード構成でキューイングを利用する場合は、以下を参考に[BackgroundJobs.json](../setup/parameters/backgroundjobs-json.md)のパラメータWorkerCountに適切な値を設定してください。

なお、シングルテナント環境での注意事項は、以下のマニュアルを参照してください。

-   「[キューイング機能：マルチノード構成下における運用の注意事項](../setup/additional/performance/queuing-manage-jobs-multi-node.md)」

### ワーカー

ワーカーやワーカー数を指定するパラメータ「WorkerCount」の詳細は、「[マルチテナント管理機能：キューイング](manage-multi-tenant-cueuing.md)」を参照してください。

### WorkerCount設定時の注意

#### すべてのノードでWorkerCountに同じ値を設定してください（必須）

クラスタリング有効時、ワーカーの登録は全ノードで共有されます。各ノードは起動時に、自ノードのWorkerCountから算出した登録以外を削除します。そのためノード間でWorkerCountの値が異なると、各ノードが起動のたびに互いの登録を削除し合い、登録が安定しません。削除が発生した場合は警告がシステムログに記録されます。

#### スレッド枠に余裕を持たせてください

ワーカーは[BackgroundService.json](../setup/parameters/background-service-json.md)で有効・無効を切り替えるリマインダーやLDAP同期などとスレッド枠を共有します。遅延なく各サービスを起動するには、[BackgroundService.json](../setup/parameters/background-service-json.md)で有効化したサービスの数にWorkerCountを加えた数を[Quartz.json](../setup/parameters/quartz-json.md)のパラメータClustering.MaxConcurrencyに対して設定してください。Clustering.MaxConcurrencyはスレッド枠の大きさを決めるパラメータで、Clustering.MaxConcurrencyの値が小さすぎる場合、起動時にシステムログへ警告が記録されます。

### 並列実行とノード間の分散

ジョブディスパッチャは1回の実行（[BackgroundJobs.json](../setup/parameters/backgroundjobs-json.md)のパラメータBackgroundJobDispatcherIntervalごとの定期実行）で、担当するテナントごとに待機中のジョブを1件ずつ取得し、並行して実行します。同一テナントのジョブは常に1件ずつ順番に実行されます（テナント単位の直列実行）。

したがって、同時に実行されるジョブの数は、担当するテナントのうち待機中のジョブを持つテナントの数で決まります。ノードの台数では決まりません。

ワーカー数は[BackgroundJobs.json](../setup/parameters/backgroundjobs-json.md)のWorkerCountで指定します。既定値（未設定）は1です。

WorkerCountが1の場合、1つのジョブディスパッチャがすべてのテナントを担当するため、ジョブの実行負荷はそれを実行している1ノードに集中します。ノードを追加しても、集中する先のノードが変わるだけで負荷は分散しません。

WorkerCountを2以上にすると、テナントIDをWorkerCountで割った余りによって、各テナントがいずれかのワーカーへ振り分けられます。ワーカーが別々のノードで実行されれば、ジョブの実行負荷がノード間に分かれます。ただし、どのノードがどのワーカーを実行するかは発火のたびに決まるため、特定のノードに固定されず、均等に配分されることも保証されません。

ノードを増やすことで得られる効果は、次の2点です。

1. 可用性（冗長化）：稼働中のノードが停止した場合、別のノードがジョブディスパッチャの処理を引き継ぎます。
1. 負荷の分散：WorkerCountを2以上に設定した場合に限り、ジョブの実行負荷が複数ノードに分かれます。単一ノードのCPU・メモリが処理の上限になっていた環境では、処理時間の短縮が見込めます。

ノードの追加は、同時に実行できるジョブの件数そのものを増やす仕組みではありません。WorkerCountを増やさずにノードだけを追加しても、処理時間はほとんど変わりません。

## 対応バージョン

|対応バージョン|内容|
|---|---|
|1.5.8.0 以降|機能追加|
