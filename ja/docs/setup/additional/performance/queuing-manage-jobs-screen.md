---
title: ジョブの管理画面
category: 追加設定：パフォーマンス
order: '0'
status: ''
parts: ''
urlstring: queuing-manage-jobs-screen
translationKey: queuing-manage-jobs-screen
shortname: ジョブの管理画面
created: 2026-06-26
updated: 2026-09-08
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/02cb2ba6edab487db830646961d907d9.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/d2da9a205bd44c6288b5e4badf32d3e4.svg#only-dark)](https://pleasanter.org/support/)

（本機能は[Extensionsトライアル](../../../products-info/extensions-trial/index.md)で試用可能です）

## 概要

「ジョブの管理画面」は、キューへ登録されたジョブの一覧を表示し、ジョブに対して様々な操作を実行できます。キューへ登録された各ジョブにはIDが振られ、先に登録されたジョブから順に実行されます。

## 前提条件

1. [BackgroundJobs.json](../../parameters/backgroundjobs-json.md)のパラメータBackgroundQueueをtrueに設定し、キューイングを有効化してください。

## 操作手順

レコードの「[エクスポート](../../../users-guide/table/record-authoring/data-analysis/table-record-export.md)」など、キューイングに対応した操作を実行します。ジョブがキューイングされ、コマンドボタンエリアの上に「バックグラウンドジョブに登録しました。(ID:n)」（nはジョブのID）というメッセージが表示されます。

### 1. 閲覧

1. ナビゲーションメニューの「バックグラウンドジョブ」を選択するか、メッセージ中のジョブIDをクリックしてください。
1. 「ジョブ管理画面」が開き、キューへ登録されたジョブが「ジョブ登録日時」の昇順に表示されます。
1. レコードの「[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)」と同様に、フィルタで表示を絞り込んだり、並び替えたりできます。

![ジョブの管理画面。キューへ登録されたジョブが一覧表示されている](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/cc539347bdb84dd89b7ef6d424e3fcd3.png)

|列名|説明|
|:--|:--|
|ID|ジョブ固有の番号を表示します。|
|ジョブ種別|画面操作のうちキュー管理対象となる処理の種類を表示します。<br>（バージョン1.5.6.0リリース時点ではインポートのみ。今後、一括削除・一括更新・サマリ同期などを追加予定）|
|状況|ジョブの管理画面を開いた時点のジョブの状況を表示します。|
|サイトID|キュー管理対象の操作を行ったサイト（テーブル）のIDを表示します。|
|サイトタイトル|キュー管理対象の操作を行ったサイトのタイトルを表示します。|
|登録ユーザ|ジョブを登録したユーザのユーザ名を表示します。|
|ジョブ登録日時|キューに登録された日時を表示します。|
|結果メッセージ|ジョブの状況に応じて、下記「[結果メッセージ](#result-msg)」に記載の内容を表示します。|
|ファイル|ジョブの完了時にファイルを出力するジョブの場合、出力ファイルのダウンロードリンクを表示します。ジョブのレコードを残したまま出力ファイルを削除した場合は「ダウンロード可能なファイルなし」と表示します。|

<a id="result-msg"></a>

### 結果メッセージ

結果メッセージには、以下の情報が表示されます。

1. {ジョブ種別}の部分には、たとえば「 エクスポート 」のようなジョブ種別の表示名が入ります。適宜読み替えてください。

|結果メッセージ|表示内容|
|:--|:--|
|{ジョブ種別}をキャンセルしました。|ジョブのキャンセル時|
|{ジョブ種別}が完了しました。|ジョブの実行完了時|
|ジョブの実行中にサービスが再起動されました。自動再実行を防ぐため、失敗として記録しました。|ジョブの実行中にプリザンターが再起動し、エラーとした場合。|
|既定のジョブ実行時間を超過しています。必要に応じて「次のジョブを実行」をクリックしてください。|ジョブの実行時間がパラメータで設定した閾値を超えた場合。[キューイング](queuing-manage-jobs.md)の「[実行時間が長いジョブへの対応](queuing-manage-jobs.md#long-runtime-jobs)」を参照。|
|バックグラウンドでのエクスポートに失敗しました。|エクスポートエラー時|

### 2. ダウンロード

バックグラウンドジョブが「完了」すると、エクスポートのようなジョブ種別では、指定したフォルダに出力ファイルが保存されます。保存が完了すると、「ファイル」列に出力ファイルへのリンクが生成されます。リンクをクリックすると出力ファイルをダウンロードできます。

![ジョブの管理画面の「ファイル」列。出力ファイルへのリンクが表示されている](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/6d3e46f5ba0b498dbb13976e6072fb7b.png)

「 状況 」が「完了」にも関わらず、ダウンロード可能なファイルを確認できないときは「ダウンロード可能なファイルなし」と表示されます。

出力ファイルの保存先は、[BackgroundJobs.json](../../parameters/backgroundjobs-json.md)のパラメータOutputFilePathで指定します。

### 3. キャンセル

「 状況 」が「待機」のバックグラウンドジョブをキャンセルできます。「実行中」のバックグラウンドジョブはキャンセルできません。

1. 画面左のチェックボックスをクリックし、キャンセルするバックグラウンドジョブを選択してください。
1. コマンドボタンエリアの「キャンセル」ボタンをクリックしてください。
1. 選択したバックグラウンドジョブがキャンセルされます。

### 4. 削除

「 状況 」が「実行中」以外のバックグラウンドジョブを削除できます。たとえば「 エクスポート 」のような出力ファイルを生成するバックグラウンドジョブでは、バックグラウンドジョブの削除と同時に、出力ファイルも削除されます。

1. 画面左のチェックボックスをクリックし、削除するバックグラウンドジョブを選択してください。
1. コマンドボタンエリアの「[一括削除](../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)」ボタンをクリックしてください。
1. 選択したバックグラウンドジョブが削除されます。

なお、[BackgroundService.json](../../parameters/background-service-json.md)の下記パラメータを設定することで、保存期間を過ぎた古いバックグラウンドジョブを自動削除することもできます。

1. DeleteBackgroundJobs
1. DeleteBackgroundJobsTime
1. BackgroundJobsRetentionPeriod

### 5. 情報の更新

 画面表示を更新したい場合は、再読み込みしてください。

### 6. 詳細画面

各レコードをクリックすると、バックグラウンドジョブの詳細画面が開きます。

![バックグラウンドジョブの詳細画面](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/7875cfaea6c2419db34da0afd6e46c14.png)

詳細画面では、以下の操作を行えます。

|No| 操作 |
|--:| :-- |
|1|出力ファイルのダウンロード |
|2| 表示中のジョブの削除 |
|3| 表示中のジョブのキャンセル |

## 対応バージョン

| 対応バージョン | 内容 |
| :-- | :-- |
| 1.5.6.0 以降 | 機能追加 |
| 1.5.7.0 以降 | 対応するジョブ種別に「[インポート](../../../users-guide/table/record-authoring/create-records/table-record-import.md)」を追加 |

## 関連情報

-   [キューイング](queuing-manage-jobs.md)
