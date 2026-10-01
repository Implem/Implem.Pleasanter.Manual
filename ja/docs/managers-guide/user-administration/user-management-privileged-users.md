---
title: 特権ユーザの設定
category: ユーザ管理機能
order: '60'
status: ''
parts: ''
urlstring: user-management-privileged-users
translationKey: user-management-privileged-users
shortname: 特権ユーザ
created: 2021-04-26
updated: 2025-09-16
---

## 概要

特権ユーザを設定します。「特権ユーザ」は、プリザンターの権限設定に関わらず全てのリソースに対して全ての権限を有する特別なユーザです。「特権ユーザ」は「パラメータファイル」、[Security.json](../../setup/parameters/security-json.md)で設定を行う必要があります。プリザンターをインストールした直後に「特権ユーザ」は存在しません。プリザンターをインストールした直後に存在する「Administrator」は[テナント管理者](user-management-tenant-manager.md)権限を有していますが「特権ユーザ」ではありません。

## 特権ユーザだけが持つ権限

-   アクセス権のないサイトへのアクセス
-   「スイッチユーザ」
-   トップ画面のごみ箱の操作
-   [システムログ](../system-log-administration/index.md)の表示
-   自分でロックしていない[テーブルのロック](../manage-table/editor/allow-lock-table/index.md)の解除
-   自分でロックしていない[レコードのロック](../manage-table/editor/editor-settings/advanced-settings/general/table-management-record-lock.md)の解除
-   [ユーザ招待](user-invite.md)機能を使用した際のユーザの承認
-   バージョン管理画面にDB使用量を表示
-   プリザンターを再起動せずにParametersフォルダ配下の情報を再読み込み
-   [バックグラウンドサーバスクリプト](../tenant-administration/background-server-script.md)の設定

## 制限事項

1.  本設定を行うにはプリザンターの再起動が必要です。

## 事前準備

1.  本設定を行うにはサーバにログインできる必要があります。

## 操作手順

1.  プリザンターが動作するサーバにログインします。
1.  プリザンターのパラメータファイルが格納されているディレクトリ（\App_Data\Parameters）を開き[Security.json](../../setup/parameters/security-json.md)をメモ帳などで開きます。
1.  "PrivilegedUsers"に、対象とするユーザのログインIDを配列形式で指定します。
1.  ファイルを保存してプリザンターを再起動します。

``` json linenums="1" title="JSON"
{
    "PrivilegedUsers": ["Administrator", "AdminUser1", "AdminUser2"]
}
```

## 関連情報

-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
-   [ユーザ管理機能：テナント管理者の設定](user-management-tenant-manager.md)
-   [システムログ管理機能](../system-log-administration/index.md)
-   [テーブルの管理：エディタ：テーブルのロックを許可](../manage-table/editor/allow-lock-table/index.md)
-   [テーブルの管理：エディタ：レコードのロックを許可](../manage-table/editor/editor-settings/advanced-settings/general/table-management-record-lock.md)
-   [ユーザ管理機能：ユーザ招待](user-invite.md)
-   [テナント管理機能：バックグラウンドサーバスクリプト](../tenant-administration/background-server-script.md)
