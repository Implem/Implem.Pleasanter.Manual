---
title: パラメータの編集
category: パラメータ管理機能
order: '200'
status: ''
parts: ''
urlstring: manage-parameter-edit
translationKey: manage-parameter-edit
shortname: パラメータ管理機能：パラメータの編集
created: 2026-06-04
updated: 2026-06-09
---
## 概要

本ページでは、プリザンター画面上で、パラメータ設定内容を閲覧、編集、保存する機能について説明します。

## 注意事項

1.  本機能を使用した場合、パラメータの変更内容は、すべてデータベースへ保存されます。
1.  データベースには変更の差分だけが保存されます。
1.  本機能でパラメータを変更しても、パラメータファイルは変更されません。
1.  <span class="pl-attention">**本機能では画面での設定が優先されますが、[Security.json](../../setup/parameters/security-json.md)のPrivilegedUsersだけは同等に扱われます**</span>

       ![画面での設定とパラメータファイルの優先関係を示す図](https://pleasanter.org/files/images/ja/managers-guide/manage-parameter/assets/7907f1facb1d44e0be785d17f3579692.png)

## 制限事項

1.  「[特権ユーザ](../user-administration/user-management-privileged-users.md)」のみ利用できます。
1.  本機能を有効化するには、[ParameterSetting.json](../../setup/parameters/parametersettings-json.md)のパラメータEnableScreenManagementをtrueに設定する必要があります。
1.  下表のパラメータファイルは起動前に確定している必要があるため、画面からは編集できません。

    | パラメータファイル名  | 理由                   |
    | :-------------------- | :--------------------- |
    | Rds.json              | データベース接続設定   |
    | ParameterSetting.json | 本機能自体の有効化設定 |
    | Migration.json        | マイグレーション設定   |

## 操作手順

### 1. 機能の有効化

1.  [ParameterSetting.json](../../setup/parameters/parametersettings-json.md)のEnableScreenManagementをtrueに変更してください。
1.  画面上に「再起動」ボタンを配置する場合は[ParameterSetting.json](../../setup/parameters/parametersettings-json.md)のEnableRestartをtrueに変更してください。
1.  従来の手順でアプリケーションを再起動してください。

### 2. パラメータ管理画面を開く

1.  [特権ユーザ](../user-administration/user-management-privileged-users.md)でログインしてください。
1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  「パラメータの管理」をクリックしてください。

    ![「管理」メニューを開いたナビゲーションメニュー。「パラメータの管理」が並ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-parameter/assets/f9eb5a0efb9d45a393b1ae59197c5790.png)

「管理画面」（{サーバ名}/Admins）で「パラメータ」を選択しても開けます。  
パラメータ管理画面には「パラメータ」のパンくずリストが表示されます。

![「パラメータ」のパンくずリストが表示されたパラメータ管理画面](https://pleasanter.org/files/images/ja/managers-guide/manage-parameter/assets/816d1ea221594e9aa4fa26b6bf2f0aba.png)

### 3. パラメータの編集

パラメータ管理画面は以下の項目で構成されています。

![パラメータ管理画面の構成。各項目に番号が振られている](https://pleasanter.org/files/images/ja/managers-guide/manage-parameter/assets/148e8a5a2e684e14bfeed3ec0e3af6b1.png)

| No. | 項目                   | 説明                                                                                                                             |
| --: | :--------------------- | :------------------------------------------------------------------------------------------------------------------------------- |
|   1 | パラメータ名           | 編集対象のパラメータファイル名です。                                                                                             |
|   2 | バージョン             | バージョン番号を格納する項目です。バージョン番号はバージョンアップ時に1ずつ増加します。                                          |
|   3 | 内容                   | パラメータの設定内容の閲覧・編集を行う領域です。ここには、パラメータファイルとDBに格納された差分をマージした内容が表示されます。 |
|   4 | 新バージョンとして保存 | パラメータの変更後に「更新」すると、常に新バージョンとして保存されます。                                                         |

1.  「パラメータ名」から、編集したいパラメータファイルを選択してください。
1.  パラメータファイルからは画面で未変更のパラメータが、DBからは画面で変更したパラメータがマージされ、[内容](../manage-table/editor/editor-settings/columns/table-management-body.md)項目に表示されます。

       ![「内容」項目にパラメータの設定内容が表示されたパラメータ管理画面](https://pleasanter.org/files/images/ja/managers-guide/manage-parameter/assets/7b3d3a629e314973ae89875e4887bdb9.png)

1.  適宜設定値を変更してください。

### 4. パラメータの保存

1.  コマンドボタンエリアの「更新」をクリックしてください。データベースへ差分が保存されます。  
       「入力されたJSONが正しくありません。」というエラーが表示される場合は、「[JSON形式のチェック](../../FAQ/features-for-developers/faq-json-format.md)」を参考に、見直してください。

       ![パラメータ管理画面のコマンドボタンエリアにある「更新」ボタン](https://pleasanter.org/files/images/ja/managers-guide/manage-parameter/assets/4861e5c2a99c43db978a1edc21011db9.png)

1.  変更をすぐに反映したい場合は、コマンドボタンエリアの「再起動」ボタンをクリックしてください。変更はアプリケーションを再起動するまで反映されません。「再起動」ボタンが表示されていない場合は、[パラメータ管理機能：画面からの再起動](manage-parameters-reboot-from-screen.md)を確認してください。

## 関連ページ

-   [Security.json](../../setup/parameters/security-json.md)
-   [ParameterSetting.json](../../setup/parameters/parametersettings-json.md)
-   [特権ユーザ](../user-administration/user-management-privileged-users.md)
-   [内容](../manage-table/editor/editor-settings/columns/table-management-body.md)
-   [パラメータ管理機能：画面からの再起動](manage-parameters-reboot-from-screen.md)
