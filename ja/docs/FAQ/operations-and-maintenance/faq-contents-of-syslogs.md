---
title: システムログ(SysLogsテーブル)の内容について
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-contents-of-syslogs
translationKey: faq-contents-of-syslogs
shortname: SysLogsテーブル
created: 2020-12-15
updated: 2026-08-07
---

## 概要

ユーザの操作結果はデータベース(Implem.Pleasanter)の中にある「[SysLogsテーブル](faq-view-syslogs.md)」へ出力されております。  出力されるログの内容は以下の通りです。  

## ユーザの特定について

|項目|内容|
|:---|:---|
|UserHostName|アクセス元のIPが記録されますが、プロキシ等を経由している場合、同一IPとなる可能性があります。|
|UserHostAddress|上記と同様です。|
|Creator|ユーザがログインしている場合、ユーザIDを示します。ユーザ名はUsersテーブルと紐づけて確認する必要があります。|
|Updator|上記と同様です。|

## ユーザの操作について

|項目|内容|
|:---|:---|
|Url|ユーザが要求したURLが記録されます。|
|UrlReferer|ユーザが１つ前に開いていたリンク元のURLが記録されます。|
|HttpMethod|ユーザが送信したHTTPメソッドが記録されます。|
|RequestData|ユーザが送信したフォームデータをエンコードした文字列が記録されます。|

## その他の項目の説明は以下の通りです

|項目|内容|
|:---|:---|
|CreatedTime|ログの記録日時です。|
|SysLogId|ログの一意なIDです。|
|Ver|ログのバージョンですが、使用していません。|

## ＜ログの種類＞

|SysLogType|ログの種類|
|:---|:---|
|10|Info|
|50|Warning|
|60|UserError|
|80|SystemError|
|90|Exception|

## ＜ログの項目＞

|項目|内容|
|:---|:---|
|OnAzure|Azure WebAppで動作させると1が記録されます。|
|MachineName|プリザンターのWebサーバのホスト名が記録されます。|
|ServiceName|サービス名「Implem.Pleasanter」が記録されます。|
|TenantName|マルチテナントにおけるテナント名が記録されます。一般の環境では対象外です。|
|Application|ログを出力しているアプリケーションのプロジェクト名が記録されます。|
|Class|ユーザが要求したコントローラー名が記録されます。（URLの一部です）|
|Method|ユーザが要求したアクション名が記録されます。（URLの一部です）|
|RequestSize|POSTされたデータのサイズが記録されます。|
|ResponseSize|サーバから返却されたデータのサイズが記録されます。|
|Elapsed|サーバサイドで1リクエスト当たりに必要とした時間（ミリ秒）が記録されます。|
|ApplicationAge|アプリケーションが開始してから経過した時間（ミリ秒）が記録されます。|
|ApplicationRequestInterval|前回の要求からのインターバル時間（ミリ秒）が記録されます。|
|SessionAge|セッションが開始してから経過した時間（ミリ秒）が記録されます。|
|SessionRequestInterval|前回、同一セッションの要求からのインターバル時間（ミリ秒）が記録されます。|
|WorkingSet64|プロセスに割り当てられた物理メモリの量（バイト）が記録されます。|
|VirtualMemorySize64|プロセスに割り当てられた仮想メモリの量 (バイト) が記録されます。|
|ProcessId|プロセスIDが記録されます。|
|ProcessName|プロセス名が記録されます。|
|BasePriority|プロセスの基本優先順位を記録します。|
|UserLanguage|ユーザの言語を記録します。|
|UserAgent|ユーザのブラウザを記録します。|
|SessionGuid|セッションを識別するためのGUIDが記録されます。|
|ErrMessage|エラー発生時のメッセージが記録されます。|
|ErrStackTrace|エラー発生時のスタックトレースが記録されます。|
|IsDebug|開発環境でデバッグ実行をした際に1が記録されます。|
|AssemblyVersion|プリザンターのバージョンが記録されます。|
|Comments|[SysLog.json](../../setup/parameters/sys-log-json.md)のClientIdをtrueに設定した場合、ログイン、ログアウト時にClientIdが記録されます。|
|UpdatedTime|ログを更新した日時が記録されます。|

## 拡張項目について

[システムログの拡張機能](../../managers-guide/system-log-administration/syslog-extension.md)により追加される項目は以下のとおりです。

|項目|内容|
|:---|:---|
|Api|APIからのリクエストの場合は「1」、そうでない場合は「0」が記録されます。|
|SiteId|参照先の「サイトID」が記録されます。|
|ReferenceId|参照先がテーブルの場合は「サイトID」、レコードの場合は「レコードID」が記録されます。|
|ReferenceType|参照種別に合わせて「Sites」、「Issues」、「Results」、「Wikis」が記録されます。|
|Status|ステータスコードが記録されます。|
|Description|ソースコード上の「クラス名.メソッド名:line 行番号:画面に表示されるメッセージ」が記録されます。|

## 関連情報

-   [パラメータ設定：SysLog.json](../../setup/parameters/sys-log-json.md)
-   [システムログの拡張機能](../../managers-guide/system-log-administration/syslog-extension.md)