---
title: 管理者パスワードを忘れたためパスワードを強制的に初期化したい
category: FAQ：ログイン
order: '0'
status: ''
parts: ''
urlstring: faq-forget-password
translationKey: faq-forget-password
shortname: ''
created: 2019-08-26
updated: 2024-04-29
---

## 回答

UPDATE文を実行してください。

---

## 概要

[パスワードのリセット](../../managers-guide/user-administration/user-password-reset.md)は、通常、テナント管理者が[パスワードのリセット](../../managers-guide/user-administration/user-password-reset.md)ボタンをクリックして操作します。しかし、テナント管理者自身がパスワードを忘れてしまったなど、画面からパスワードを変更できない場合は、データベースに対して以下のSQLを実行することでパスワードを変更できます。

!!! tip "「パスワードのリセット」ボタン"
    [ユーザの管理](../../managers-guide/user-administration/index.md)画面を開き、該当ユーザの編集画面に配置されています。

## 制限事項

1.  この手順はプリザンター自身でログインユーザ、パスワードを管理している場合に有効な手順です。LDAP認証やSAML認証を設定している場合は、接続先のLDAP、SAMLの管理者に問い合わせてください。
1.  この手順はご自身でプリザンターを構築した場合の手順です。Pleasanter.netのユーザがパスワードを変更したい場合は、以下のリンク先を参照してください。  
    [FAQ：Pleasanter.netのパスワードを忘れたためパスワードを初期化したい](../pleasanter.net/faq-pleasanter-net-forget-password.md)

## 操作手順

1.  プリザンターをインストールしているサーバにログインしてください。
1.  [SSMS](../../setup/installation/install-database/install-sql-server-management-studio.md)（SQL Server Management Studio）を起動してください。
1.  「オブジェクトエクスプローラ」から「データベース」を展開し、「Implem.Pleasanter」を選択してください。
1.  「Implem.Pleasanter」を右クリックし、「新しいクエリ」をクリックしてください。
1.  下記サンプルコードに記載のSQLを実行してください。
1.  変更したパスワードでプリザンターにログインしてください。
1.  ログイン後、再度ユーザの設定などを行ってください。

## サンプルコード

-   以下のSQLはSQL Server専用です。
-   「パスワードを変更するユーザID」は実際のユーザIDに置き換えてください。
-   「変更後のパスワード」は変更したいパスワード（半角英数、数値、記号）に置き換えてください。

    ``` sql title="パスワードのリセット" linenums="1"
    USE [Implem.Pleasanter]

    DECLARE @password NVARCHAR(128) = '変更後のパスワード'

    UPDATE [Users]
    SET [Password] = (
        SELECT LOWER(CONVERT(
            NVARCHAR(128),
            HASHBYTES('SHA2_512', CAST(@password AS VARCHAR(128))),
            2
        ))
    )
    WHERE LoginId = 'パスワード変更するユーザID';
    ```

## 関連情報

-   [ユーザ管理機能：パスワードリセット](../../managers-guide/user-administration/user-password-reset.md)
-   [ユーザ管理機能](../../managers-guide/user-administration/index.md)
-   [FAQ：Pleasanter.netのパスワードを忘れたためパスワードを初期化したい](../pleasanter.net/faq-pleasanter-net-forget-password.md)
-   [SQL Server Management Studioのインストール](../../setup/installation/install-database/install-sql-server-management-studio.md)
