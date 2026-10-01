---
title: 画面からの再起動
category: パラメータ管理機能
order: '300'
status: ''
parts: ''
urlstring: manage-parameters-reboot-from-screen
translationKey: manage-parameters-reboot-from-screen
shortname: パラメータ管理機能：画面からの再起動
created: 2026-05-29
updated: 2026-06-09
---

## 概要

[パラメータ管理画面](manage-parameter-edit.md)に「再起動」ボタンを表示させることができます。「[特権ユーザ](../user-administration/user-management-privileged-users.md)」が「再起動」ボタンをクリックすると、プリザンターの画面からプリザンターのプロセスを停止することができます。

また、[パラメータ管理機能：環境別の自動再起動設定](manage-parameters-auto-reboot-settings.md)を実施することで、プロセス停止に伴う自動再起動が可能となります。[パラメータ管理機能：冗長化構成におけるパラメータ設定の連携](manage-parameter-redundant-sync.md)を実現するためには、この自動再起動設定が必須です。

## 制限事項

1. パラメータ管理画面の「再起動」ボタンはアプリケーションの停止のみを担います。
1. 起動プロセス管理が設定されていない環境（dotnetコマンドで手作業で起動している場合など）では、自動的に再起動しません。停止後に手動でアプリケーションを起動してください。
1. 本機能を冗長化構成で利用する場合は、必ずIIS、systemd、Docker等の起動プロセス管理下で運用してください。
1. 本機能でいう冗長化構成は、2台のWebサーバが1台のDBを参照する構成に限ります。

## 操作手順

### 1. 「再起動」ボタンの設置

1. [ParameterSetting.json](../../setup/parameters/parametersettings-json.md)のEnableRestartをtrueに設定してください。
1. [パラメータ管理画面](manage-parameter-edit.md)の下部に「再起動」ボタンが表示されます。

### 2. 自動再起動の設定

[パラメータ管理機能：環境別の自動再起動設定](manage-parameters-auto-reboot-settings.md)の手順を実施してください。

### 3. 再起動の実行

1. [パラメータ管理画面](manage-parameter-edit.md)下部の「再起動」ボタンをクリックしてください。
1. 確認ダイアログ「再起動中はシステムを利用できません。本当に再起動しますか？」が表示されるのでクリックしてください。アプリケーションの停止処理が開始されます。
1. 「システムを再起動します。」というメッセージが表示され、約2秒後にアプリケーションが停止します。
1. 起動プロセス管理ツールにより自動的に再起動されます。

## 冗長化構成下での再起動

2台のWebサーバが1台のDBを参照する構成では、1台のWebサーバでパラメータを変更・保存して再起動すると、もう1台のWebサーバの再起動により、パラメータの変更が自動的に反映されます。

詳細は[パラメータ管理機能：冗長化構成におけるパラメータ設定の連携](manage-parameter-redundant-sync.md)を参照してください。

## 関連情報

-   [パラメータ管理機能：パラメータの編集](manage-parameter-edit.md)
-   [パラメータ管理機能：環境別の自動再起動設定](manage-parameters-auto-reboot-settings.md)
-   [パラメータ管理機能：冗長化構成におけるパラメータ設定の連携](manage-parameter-redundant-sync.md)

## 冗長化構成の関連情報

冗長化構成については、以下の各マニュアルも併せて確認してください。

-   [追加設定：クラスタ化への備え：ASP.NET Coreデータ保護キーを外部保存する](../../setup/additional/ready-for-clustering/data-protection-key-store.md)
-   [追加設定：クラスタ化への備え：ウォームアップ機能](../../setup/additional/ready-for-clustering/warmup.md)
-   [追加設定：クラスタ化への備え：クラスタ構成で添付ファイルをローカルストレージ格納する設定](../../setup/additional/ready-for-clustering/clustering-attachments-store-local-storage.md)
-   [追加設定：クラスタ化への備え：バックグラウンドサービスを複数インスタンス構成に対応させる](../../setup/additional/ready-for-clustering/service-clustering.md)
-   [追加設定：クラスタ化への備え：冗長化構成におけるパラメータ設定の連携](../../setup/additional/ready-for-clustering/clustering-parameter-redundant-sync.md)
-   [追加設定：クラスタ化への備え：添付ファイルのアップロード・登録に関する設定](../../setup/additional/ready-for-clustering/clustering-attachment-item-settings.md)