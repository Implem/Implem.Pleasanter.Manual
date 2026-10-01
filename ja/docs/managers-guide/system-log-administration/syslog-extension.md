---
title: システムログの拡張機能
category: システムログ管理機能
order: '200'
status: ''
parts: ''
urlstring: syslog-extension
translationKey: syslog-extension
shortname: システムログの拡張機能
created: 2023-07-07
updated: 2024-09-13
---

## 概要

パラメータ設定：[Rds.json](../../setup/parameters/rds-json.md)の設定により、システムログを拡張することが可能です。APIからの要求であるか、要求先のサイトID、レコードID、HTTPステータス等を記録することができます。

## 注意事項

1.  CodeDefiner実行時は、データベースのバックアップを取得してから実施してください。現状のSysLogsテーブルのレコード件数が多い場合は、CodeDefinerの実行に時間がかかる可能性があります。
1.  パラメータ設定：[Rds.json](../../setup/parameters/rds-json.md)の「SysLogsSchemaVersion」を「2」に変更後、再度「1」に変更した場合は追加カラムが削除されます。パラメータファイルのマージを誤らないようにしてください。

## 制限事項

1.  ステータスコード「401」は[SysLog.json](../../setup/parameters/sys-log-json.md)の「LoginFailure」がtrueの場合のみ記録されます。
1.  ステータスコード「403」は、記録テーブルおよび期限付きテーブルにアクセスした場合のみとなります。権限のないユーザがフォルダにアクセスした場合は「404」として記録されます。

## 前提条件

1.  [システムログの管理](index.md)画面から参照する場合は[特権ユーザ](../user-administration/user-management-privileged-users.md)の権限が必要です。

## 設定手順

1.  パラメータ[Rds.json](../../setup/parameters/rds-json.md)の「SysLogsSchemaVersion」を「2」に変更します。
1.  CodeDefinerを実行します。
1.  コンソールにSysLogsテーブルの定義変更が行われたログが出力されることを確認します。
1.  SysLogsテーブルを確認し、カラムが追加されたことを確認します。

### CodeDefiner実行結果

``` cmd
> dotnet Implem.CodeDefiner.dll _rds
<INFO> UsersConfigurator.Execute: Implem.Pleasanter_Owner
<INFO> UsersConfigurator.Execute: Implem.Pleasanter_User
～中略～
<INFO> Tables.MigrateTable: SysLogs
<INFO> Tables.CreateTable: SysLogs
<INFO> Tables.MigrateTable: SysLogs
<INFO> Tables.CreateTable: SysLogs_deleted
<INFO> Tables.MigrateTable: SysLogs
<INFO> Tables.CreateTable: SysLogs_history
～中略～
<SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
<SUCCESS> Starter.Main: All of the processes have been completed.
```

## 追加カラムについて

システムログの拡張により追加されるカラムは以下のとおりです。

| カラム名      | 値の例   | 説明                                                                                           |
| :------------ | :------- | :--------------------------------------------------------------------------------------------- |
| Api           | 1        | APIからのリクエストの場合は「1」、そうでない場合は「0」が記録されます。                        |
| SiteId        | 9999     | 参照先の「サイトID」が記録されます。                                                           |
| ReferenceId   | 9999     | 参照先がテーブルの場合は「サイトID」、レコードの場合は「レコードID」が記録されます。           |
| ReferenceType | Results  | 参照種別に合わせて「Sites」、「Issues」、「Results」、「Wikis」が記録されます。                |
| Status        | （後述） | ステータスコードが記録されます。                                                               |
| Description   | （後述） | ソースコード上の「クラス名.メソッド名:line 行番号:画面に表示されるメッセージ」が記録されます。 |

## ステータスコードと詳細について

以下のいずれかのステータスコードが出力されます。

| Statusの値 | 説明                                          | Descriptionの例                                                                                                |
| :--------- | :-------------------------------------------- | :------------------------------------------------------------------------------------------------------------- |
| 200        | OK：リクエストが正常に処理できたとき          | (NULL)                                                                                                         |
| 400        | Bad Request：一般的な操作エラー               | ResultValidators.OnUpdating:line 514:レコード 99999 は Administrator が 2023/07/07 12:00:00 にロックしました。 |
| 401        | Unauthorized：認証に失敗したとき              | UserModel.LoginFailureLog:line 4403:指定されたログインIDまたはパスワードが不正です。                           |
| 403        | Forbidden：権限がないサイトへアクセスしたとき | ResultValidators.OnCreating:line 216:指定された情報は見つかりませんでした。                                    |
| 404        | Not Found：Webページが見つからないとき        | ItemModel.Index:line 228:指定された情報は見つかりませんでした。                                                |

## 関連情報

-   [パラメータ設定：Rds.json](../../setup/parameters/rds-json.md)
-   [システムログ管理機能](index.md)
-   [特権ユーザ](../user-administration/user-management-privileged-users.md)
