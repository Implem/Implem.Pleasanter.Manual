---
title: レートリミット
category: 追加設定：パフォーマンス
order: '100'
status: ''
parts: ''
urlstring: ratelimit
translationKey: ratelimit
shortname: ''
created: 2026-06-19
updated: 2026-07-14
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/02cb2ba6edab487db830646961d907d9.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/d2da9a205bd44c6288b5e4badf32d3e4.svg#only-dark)](https://pleasanter.org/support/)

（本機能は[Extensionsトライアル](../../../products-info/extensions-trial/index.md)で試用可能です）

## 概要

「レートリミット機能」は、特定の利用者・IPアドレス・APIキー単位で、過剰なリクエスト（短時間の大量な画面操作や、エクスポート・インポートなどの重い処理の集中実行）を抑制し、システムの安定稼働を支える機能です。一時的なアクセス集中（バースト）の許容、一定時間内の実行回数制限、同時実行数制限などを柔軟に設定でき、利用環境に応じた負荷制御を実現します。

設定はパラメータファイル[RateLimit.json](../../parameters/ratelimit-json.md)で行います。各設定項目の詳細は、パラメータマニュアル[RateLimit.json](../../parameters/ratelimit-json.md)を参照してください。

## 制限事項

1. 既定では無効（Modeが"Off"）です。利用するには[RateLimit.json](../../parameters/ratelimit-json.md)で有効化が必要です。
1. 本機能は、利用者・IPアドレス・APIキーなどの「単位ごと」に制限を行うものです。システム全体（全利用者の合算）のリクエスト総量を制限する機能ではありません。

## 動作モード

[RateLimit.json](../../parameters/ratelimit-json.md)のトップレベル「Mode」で、機能全体の動作を切り替えます。

|設定値|説明|
|:--|:--|
|Off|（既定値）機能を無効にします。性能への影響はありません。|
|LogOnly|上限超過を観測してログに記録しますが、リクエストの遮断は行いません。閾値を調整する際の観測に利用します。|
|On|上限超過時に「429 Too Many Requests」を返して遮断します。|

導入時は、まず「LogOnly」で実際のアクセス傾向を観測して閾値を調整し、その後「On」に切り替える運用を推奨します。

## 制限の単位（パーティション）

制限は以下の「単位」ごとに、独立してカウントされます。

|単位|説明|
|:--|:--|
|User|ログインユーザ（ログインID）単位。未認証のリクエストは対象外です。|
|Ip|接続元IPアドレス単位。|
|ApiKey|APIキー単位。APIキーを取得できないリクエストは、接続元IPアドレス単位にフォールバックして制限します。|
|Auto|ログインユーザ単位、未認証の場合はIP単位、というように自動で解決します。|

## ポリシー一覧

プリザンターでは、機能カテゴリごとに「ポリシー」を定義し、それぞれに上限を設定します。各リクエストは、機能カテゴリに応じたポリシーと、全経路共通の上位ポリシー「GlobalLimiter」の両方の評価を受け、いずれかの上限を超えると遮断されます。

|ポリシー名|単位|アルゴリズム|既定の上限|主な対象|
|:--|:--|:--|:--|:--|
|GlobalLimiter|Auto|TokenBucket|容量100 / 毎秒+50|全経路共通の上位ポリシー（最終防壁）|
|General|User|TokenBucket|容量10 / 毎秒+5|一般的な画面操作|
|List|User|SlidingWindow|直近60秒で30回|一覧・検索・グリッド・集計ビュー|
|Admin|User|FixedWindow|60秒ごとに30回|管理操作（ユーザ／組織／グループ管理など）|
|Heavy|User|Concurrency|同時1|画面側の重い処理（エクスポート・インポートなど）|
|ApiHeavy|ApiKey|Concurrency|同時1|API経由の重い処理|
|Api|Auto|TokenBucket|容量30 / 毎秒+10|REST API 全般|
|AnonymousIp|Ip|FixedWindow|60秒で60回|未認証アクセス（ログイン試行など）|
|PublicForm|Ip|TokenBucket|容量5 / 毎秒+2|公開フォームの送信|

各ポリシーの役割と閾値調整の考え方は、「[レートリミット機能：ポリシーと閾値の調整](ratelimit-policy-threshold-setting.md)」を参照してください。

## 制限アルゴリズム

制限アルゴリズムとは、レートリミットにおいて一定時間内に行える操作の回数を制限するためのルールです。アルゴリズムごとにアクセスの判定方法や制限の特性が異なるため、利用シーンに応じて適切な方式を選択できます。

|アルゴリズム|説明|
|:--|:--|
|TokenBucket|バケット内のトークンを消費する形で操作回数を制限する方式です。バケット内にトークンが存在する限り処理は即時許可され、枯渇した場合は拒否されます。バケット内のトークンは一定間隔で補充されます。通常の画面操作・APIに適しています。|
|FixedWindow|一定時間（ウィンドウ）ごとにカウンタをリセットし、その枠内での操作回数を制限する方式です。ウィンドウの境界付近で操作が集中すると、場合によってはレートリミットの2倍近いスループットを許容する可能性があります。|
|SlidingWindow|直近の一定期間（ウィンドウ）だけを対象に操作回数を制限する方式です。本機能ではカウンタ近似方式という、ウィンドウを複数のセグメントに分割し、セグメント単位で操作回数を制限する方式を採用しています。一般的に、Fixed Windowよりもウィンドウ境界でのバーストが発生しづらいとされています。|
|Concurrency|負荷制御に近い方式です。単位時間あたりの回数ではなく、同時実行数を制限します。同時実行開始時にカウントを増やし、完了時に減らします。|

## 上限超過時の動作

[RateLimit.json](../../parameters/ratelimit-json.md)の「Mode」が「On」のとき、上限を超えたリクエストは「429 Too Many Requests」で遮断されます。応答の形式は、呼び出し元に応じて自動的に切り替わります。

|呼び出し元|応答|
|:--|:--|
|ブラウザでの直接アクセス（画面遷移）|簡易エラーページ（HTML）を表示します。|
|画面内の操作（Ajax）|画面内にメッセージを表示します。|
|API（/api/ など）|エラーを表す JSON を返します。|

-   [RateLimit.json](../../parameters/ratelimit-json.md)の「RejectedResponse」の「IncludeRetryAfter」が true の場合、応答に「Retry-After」ヘッダ（再試行までの目安秒数）を付与します。  
-   「RateLimit.json」の「RejectedResponse」の「LogRejected」が true の場合、「Mode」が「On」での実拒否が構造化ログ（logs/{年}/{月}/{日}/ratelimitlogs.json）に記録されます。false にしても件数（メトリクス）は常に記録され、「Mode」が「LogOnly」時の仮想拒否ログは本設定に関わらず常に出力されます。  
-   拒否・仮想拒否の件数は、一定間隔（既定60秒）でポリシー別に集計され、同じログファイルに「RateLimitMetricsSnapshot」として記録されます。大量拒否で個別ログが間引かれても、件数はこの集計で把握できます。  
-   既定ではログはファイルにのみ出力されます。Docker/Kubernetes など標準出力(stdout)でログを収集する環境向けの設定方法は[レートリミット機能：拒否ログ・メトリクスの出力先設定](ratelimit-metrics.md)を参照してください。

## 設定の流れ

1. パラメータファイル[RateLimit.json](../../parameters/ratelimit-json.md)を編集します（「Mode」や各ポリシーの上限値など）。
2. プリザンターを再起動します（「RateLimit.json」は起動時に読み込まれます）。

    -   「[パラメータ管理機能](../../../managers-guide/manage-parameter/index.md)」を有効にしている場合は、画面からの編集・再起動も可能です。詳細は「パラメータ管理機能」を参照してください。

3. 「LogOnly」で実際のアクセスを観測し、誤って制限してしまう箇所がないか確認します。
4. 閾値を調整したうえで「Mode」を「On」に切り替えます。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.6.0 以降|レートリミット機能を追加|

## 関連情報

-   [レートリミット機能：拒否ログ・メトリクスの出力先設定](ratelimit-metrics.md)
