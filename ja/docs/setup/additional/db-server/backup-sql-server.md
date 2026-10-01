---
title: プリザンターのデータベース（SQL Server）をバックアップする
category: 追加設定：DBサーバ
order: '100'
status: ''
parts: ''
urlstring: backup-sql-server
translationKey: backup-sql-server
shortname: ''
created: 2019-04-29
updated: 2025-06-12
---

## スクリプトの配置

下記のスクリプトをダウンロードし、ローカルディスクに配置してください。

:fontawesome-brands-github: [DbBackup.vbs](https://github.com/Implem/Implem.Pleasanter/blob/master/Implem.Pleasanter/Tools/DbBackup.vbs)

## パラメータの変更

DbBackup.vbsをテキストエディタで開き、下記の変数の値を変更し、保存してください。

| 変数名 | 設定内容                         |
| :----- | :------------------------------- |
| server | データベースのサーバ名           |
| db     | データベースのカタログ名         |
| uid    | バックアップ権限を持ったユーザID |
| pwd    | 上記ユーザのパスワード           |
| path   | バックアップの保存先、ファイル名 |

## バックアップの実行

DbBackup.vbsを起動し、バックアップを実行してください。

!!! warning "「アクセスが拒否されました」と表示される場合"
    SQL Serverのバックアップデータの書き込みは、ログイン中のユーザではなくSQL Serverのサービスアカウントで実行されます。バックアップ先のフォルダにSQL Serverのサービスアカウントの書き込み権限を指定してください。

定期的なバックアップを行うにはOSのタスクスケジューラなどを使用してください。

!!! tip " SQL Server Standard以上のエディションを利用している場合"
    メンテナンスプランによる定期バックアップを実行できます。詳細は以下のページを参照してください。  
    [FAQ：プリザンターのDBデータを定期的にバックアップしたい（SQL Server）](../../../FAQ/backup-restore/faq-backup-schedule.md)

## 関連情報

-   [DbBackup.vbs](https://github.com/Implem/Implem.Pleasanter/blob/master/Implem.Pleasanter/Tools/DbBackup.vbs)
-   [FAQ：プリザンターのDBデータを定期的にバックアップしたい（SQL Server）](../../../FAQ/backup-restore/faq-backup-schedule.md)
