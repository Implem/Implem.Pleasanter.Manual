---
title: パラメータ管理機能
category: パラメータ管理機能
order: '100'
status: ''
parts: ''
urlstring: manage-parameter
translationKey: manage-parameter
shortname: パラメータ管理機能
created: 2026-05-29
updated: 2026-06-09
---

## 概要

パラメータ管理機能は、以下の3つの機能から成ります。

1.  プリザンターの画面上で、パラメータの設定内容を閲覧、編集、DBへ保存する機能
1.  プリザンターの画面上に「再起動」ボタンを表示し、画面からアプリケーションを再起動できるように設定する機能
1.  冗長化構成において、パラメータの設定内容を自動連携する機能

![冗長化構成でパラメータの設定内容を自動連携する仕組みを示した図](https://pleasanter.org/files/images/ja/managers-guide/manage-parameter/assets/b3672c939327405a91cd6988dfcacab0.png)

各機能の詳細は、以下のページを順に参照してください。

1.  [パラメータ管理機能：パラメータの編集](manage-parameter-edit.md)
1.  [パラメータ管理機能：画面からの再起動](manage-parameters-reboot-from-screen.md)
1.  [パラメータ管理機能：環境別の自動再起動設定](manage-parameters-auto-reboot-settings.md)
1.  [パラメータ管理機能：冗長化構成におけるパラメータ設定の連携](manage-parameter-redundant-sync.md)
1.  [パラメータ管理機能を有効化したDockerコンテナで起動する](manage-parameter-enabled-on-docker.md)

なお、本機能に関連するパラメータは[ParameterSetting.json](../../setup/parameters/parametersettings-json.md)にまとめられています。

## 前提条件

-   [パラメータ管理機能：冗長化構成におけるパラメータ設定の連携](manage-parameter-redundant-sync.md)を使用する場合は、再起動の設定（上記2.と3.）が必要です。

## 制限事項

1.  「[特権ユーザ](../user-administration/user-management-privileged-users.md)」のみ利用できます。
1.  下表のパラメータファイルは起動前に確定している必要があるため、画面からは編集できません。

      | パラメータファイル名      | 理由                   |
      | :------------------------ | :--------------------- |
      | [Rds.json](../../setup/parameters/rds-json.md)              | データベース接続設定   |
      | [ParameterSetting.json](../../setup/parameters/parametersettings-json.md) | 本機能自体の有効化設定 |
      | [Migration.json](../../setup/parameters/migration-json.md)        | マイグレーション設定   |

## 対応バージョン

| 対応バージョン    | 説明     |
| :---------------- | :------- |
| バージョン1.5.5.0 | 機能追加 |
