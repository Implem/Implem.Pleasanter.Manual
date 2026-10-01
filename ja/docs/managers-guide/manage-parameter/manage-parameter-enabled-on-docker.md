---
title: パラメータ管理機能を有効化したDockerコンテナで起動する
category: パラメータ管理機能
order: '0'
status: ''
parts: ''
urlstring: manage-parameter-enabled-on-docker
translationKey: manage-parameter-enabled-on-docker
shortname: ''
created: 2026-06-08
updated: 2026-06-12
---

## 概要

[パラメータ管理機能](index.md)を有効化したDockerコンテナを起動する手順を説明します。

## 操作手順

1. 「[Dockerイメージを使用しパラメータを既定値から変更して起動する](../../setup/installation/running-with-docker/change-parameters-at-docker-image.md)」を参照し、「1-2. パラメータファイルの準備」の3.までを実施してください。
1. [ParameterSetting.json](../../setup/parameters/parametersettings-json.md)のEnableScreenManagementとEnableRestartをtrueに設定してください。

   ##### ParameterSetting.json
   ```json
   {
       "EnableScreenManagement": true,
       "EnableRestart": true,
         : 省略
   }
   ```

1. [Security.json](../../setup/parameters/security-json.md)のPrivilegedUsersに[パラメータ管理機能](index.md)を使用するユーザのログインIDを設定してください。以下では、PrivilegedHayatoを特権ユーザに設定しています。

   ##### Security.json
   ```json
   {
         : 省略
       "PrivilegedUsers": ["PrivilegedHayato"],
         : 省略
   }
   ```

1. [パラメータ管理機能：環境別の自動再起動設定](manage-parameters-auto-reboot-settings.md)を参照し、利用環境に応じた起動プロセスを設定してください。
1. 「[Dockerイメージを使用しパラメータを既定値から変更して起動する](../../setup/installation/running-with-docker/change-parameters-at-docker-image.md)」を参照し、「1-2. パラメータファイルの準備」の5.以降を実施してください。

## 冗長化構成におけるパラメータ設定の連携

冗長化構成（2台のWebサーバが1台のDBを参照する構成）において、1台のWebサーバでパラメータを保存したとき、もう1台のWebサーバへ変更が自動的に連係される機能を利用する場合は、[パラメータ管理機能：冗長化構成におけるパラメータ設定の連携](manage-parameter-redundant-sync.md)を参照してください。

## 対応バージョン

| 対応バージョン | 内容 |
| --- | --- |
| バージョン1.5.5.0 | 機能追加 |

## 関連情報

-   [パラメータ管理機能](index.md)
-   [パラメータ管理機能：環境別の自動再起動設定](manage-parameters-auto-reboot-settings.md)
-   [パラメータ管理機能：冗長化構成におけるパラメータ設定の連携](manage-parameter-redundant-sync.md)