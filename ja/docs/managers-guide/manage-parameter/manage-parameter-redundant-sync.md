---
title: 冗長化構成におけるパラメータ設定の連携
category: パラメータ管理機能
order: '500'
status: ''
parts: ''
urlstring: manage-parameter-redundant-sync
translationKey: manage-parameter-redundant-sync
shortname: パラメータ管理機能：冗長化構成におけるパラメータ設定の連携
created: 2026-06-04
updated: 2026-06-09
---

## 概要

### 想定環境

以下のような冗長化構成（2台のWebサーバが1台のDBを参照する構成）において、1台のWebサーバでパラメータを保存したとき、もう1台のWebサーバへ変更が自動的に連携される機能について説明します。

![2台のWebサーバが1台のDBを参照する冗長化構成の図](https://pleasanter.org/files/images/ja/managers-guide/manage-parameter/assets/4cc9c1f16fbf4d27985e62587a31955f.png)

## 制限事項

1. 本機能はWebサーバ2台、DBサーバ1台の冗長化構成のみを想定しています。Webサーバが3台以上の構成では、本機能を利用できません。

## 前提条件

1. 以下のマニュアルの手順を事前に完了している必要があります。
   1. [パラメータ管理機能](index.md)
   1. [パラメータ管理機能：パラメータの編集](manage-parameter-edit.md)
   1. [パラメータ管理機能：画面からの再起動](manage-parameters-reboot-from-screen.md)
   1. [パラメータ管理機能：環境別の自動再起動設定](manage-parameters-auto-reboot-settings.md)

## パラメータ連携の流れ

以下の順序で処理が進みます。

1. WEB#1でユーザが「再起動」ボタンをクリックします。
1. WEB#1が "再起動時刻" としてDBに現在日時を保存します。この保存が、もう一方のWEB#2へのパラメータ連携シグナルになります。
1. WEB#2は次のリクエストを受け付けたタイミングで再起動時刻を確認し、WEB#2のメモリ上に保持される自身の起動日時より新しい値が設定されていれば、アプリケーションを停止します。
1. 起動プロセス管理（IIS、systemd、Dockerなど）がWEB#2のプロセスを再起動します。再起動については、[パラメータ管理機能：画面からの再起動](manage-parameters-reboot-from-screen.md)および[パラメータ管理機能：環境別の自動再起動設定](manage-parameters-auto-reboot-settings.md)を参照してください。
1. 再起動後、WEB#2は再起動時刻をNULLにクリアし、DBから最新の変更差分を取得・適用します。

## 再起動が実行される条件

WEB#2がリクエストを受け付けた際、以下の条件をすべて満たす場合にのみアプリケーションを停止します。

1. 再起動時刻の確認から120秒以上（この秒数は[ParameterSetting.json](../../setup/parameters/parametersettings-json.md)のRestartChecklntervalSecondsで変更できます）が経過している。
1. 再起動時刻がNULLでない。
1. 再起動時刻が自身の起動日時より新しい。
1. 同一サーバ内の他のスレッドがまだ再起動処理を開始していない（二重再起動防止）。

いずれか1つでも満たさない場合は再起動せず、通常処理を続行します。

## 再起動チェック間隔（RestartCheckIntervalSeconds）

WEB#2がリクエストのたびに、再起動時刻の確認を行うと、DBの負荷が増大してしまいます。そこで、各Webサーバは前回の確認日時を記録し、[ParameterSetting.json](../../setup/parameters/parametersettings-json.md)のRestartCheckIntervalSecondsに設定した秒数が経過するまでDBへの問い合わせをスキップします。

RestartCheckIntervalSecondsの設定値を検討する際には、パラメータ反映の遅延とDB負荷のトレードオフを考慮する必要があります。

| 設定値 | 影響 |
| --- | --- |
| 既定値よりも小さい値 | パラメータ保存から他サーバ再起動までの遅延が短くなる。<br>DBへの問い合わせ頻度とDB負荷が増加する。 |
| 既定値よりも大きい値 | 他サーバへの反映遅延が最大でRestartCheckIntervalSeconds秒発生する。<br>DBへの問い合わせ頻度とDB負荷が減少する。 |
| 0またはnull | 再起動しません。 |

## 再起動ループの防止

アプリケーションの起動時に再起動時刻が自動的にnullクリアされます。再起動時刻が自身の起動日時より新しい場合に再起動するため、再起動後のリクエストで再度再起動が発生する「再起動ループ」は発生しません。

## 二重再起動の防止

同じWebサーバに対して複数のリクエストが同時に到達した場合でも、排他制御によりアプリケーションの停止処理は1回だけ実行されます。

## 対応バージョン

| 対応バージョン | 内容 |
| --- | --- |
| バージョン1.5.5.0 | 機能追加 |

## 関連情報

-   [パラメータ管理機能](index.md)
-   [パラメータ管理機能：パラメータの編集](manage-parameter-edit.md)
-   [パラメータ管理機能：画面からの再起動](manage-parameters-reboot-from-screen.md)
-   [パラメータ管理機能：環境別の自動再起動設定](manage-parameters-auto-reboot-settings.md)
