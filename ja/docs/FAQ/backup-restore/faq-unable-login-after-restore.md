---
title: 別サーバでバックアップしたファイルをリストアすると接続できない（SQL Server）
category: FAQ：バックアップ、リストア
order: '600'
status: ''
parts: ''
urlstring: faq-unable-login-after-restore
translationKey: faq-unable-login-after-restore
shortname: ''
created: 2023-11-09
updated: 2024-04-29
---

## 回答

`ALTER USER`コマンドでユーザマッピングを修復してください。

---

## 概要

[FAQ：プリザンターのDBデータを定期的にバックアップしたい（SQL Server）](faq-backup-schedule.md)で取得したSQLSeverの[バックアップ](faq-backup-and-restore.md)ファイルを別の環境のプリザンターに[リストア](faq-backup-and-restore.md)した際、ユーザID、パスワードを変更していないにもかかわらずログインできなくなる場合があります。復元したデータベースのユーザとサーバのログインユーザのマッピングが不整合となっていることが原因です。

## 操作手順

1.  [FAQ：プリザンターのDBデータをバックアップする方法とリストアする方法を知りたい](faq-backup-and-restore.md)にしたがってダンプファイルをリストアしてください。
1.  SSMSにて以下SQLを実行してください。

    ```sql
    Use [Implem.Pleasanter]
    EXEC sp_change_users_login 'Report'
    ```

1.  手順2.の結果でImplem.Pleasanter_UserまたはImplem.Pleasanter_Owner（もしくは両方）が表示した場合は、以下のコマンドを実行します。

    ``` sql
    Use [Implem.Pleasanter]
    ALTER USER {ユーザ名※1} WITH LOGIN = {ユーザ名※1}
    ```

    !!! note
        -   ユーザ名は「[Implem.Pleasanter_User]」または「[Implem.Pleasanter_Owner]」と記述してください。
        -   手順2.で両方表示した場合はそれぞれのユーザに対して`ALTER USER`文を実行してください。

1.  再度手順2.のSQLを実行し、結果が表示しなくなるまで手順3.の処理を繰り返します。

## 関連情報

-   [FAQ：プリザンターのDBデータを定期的にバックアップしたい（SQL Server）](faq-backup-schedule.md)
-   [FAQ：プリザンターのDBデータをバックアップする方法とリストアする方法を知りたい](faq-backup-and-restore.md)
