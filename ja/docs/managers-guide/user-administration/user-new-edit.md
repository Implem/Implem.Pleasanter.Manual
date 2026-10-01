---
title: 作成・更新
category: ユーザ管理機能
order: '10'
status: ''
parts: ''
urlstring: user-new-edit
translationKey: user-new-edit
shortname: ''
created: 2025-02-03
updated: 2025-07-08
---

## 概要

プリザンターを利用するユーザの新規作成および更新を行います。

## 制限事項

1.  [LDAP認証](../../setup/additional/authn-authz/active-directory.md)や[SAML認証](../../setup/additional/authn-authz/saml.md)で名前や組織などのユーザ情報を取得する設定を行った場合は、本画面で更新しても認証サーバ側から取得した情報で上書きされます。
1.  登録済みユーザのパスワードを変更する際は[パスワードリセット](user-password-reset.md)を行ってください。
1.  Pleasanter.netのフリープラン、ライトプラン、スタンダードプランでは一部機能が利用可能です。詳しくは[FAQ：Pleasanter.netのユーザ管理で利用可能な機能について](../../FAQ/pleasanter.net/faq-pleasanter-net-user.md)を参照ください。

## 事前準備

-   この操作を実行するユーザは[テナント管理者](user-management-tenant-manager.md)権限を有効にしておく必要があります。

## 操作手順

### ユーザの新規作成

1.  「管理」メニューを開き[ユーザの管理](index.md)をクリックします。
1.  「新規作成」ボタンをクリックします。
1.  必要事項を入力します。
1.  「作成」ボタンをクリックします。

![ユーザの新規作成画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/52f67e495a024a6e8642f9a585d9d8d1.png)

### ユーザの更新

1.  「管理」メニューを開き[ユーザの管理](index.md)をクリックします。
1.  一覧画面で適宜検索し、更新したいユーザをクリックします。
1.  下表の必要事項を入力し、更新ボタンをクリックします。

![ユーザの編集画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/6f090ed4b94b47629347baa530eec168.png)

## 設定項目

| 項目名                       | 説明                                                                 | 設定                                                                                                                                              | その他                                                                                                                      |
| :--------------------------- | :------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------- |
| ユーザID                     | 対象ユーザのID                                                       | 一意の番号を自動採番                                                                                                                              |                                                                                                                             |
| バージョン                   | 変更履歴の番号                                                       | 更新時に自動でカウントアップ                                                                                                                      |                                                                                                                             |
| ログインID                   | システムにログインするためのID                                       | 任意のIDを設定                                                                                                                                    |                                                                                                                             |
| 名前                         | ユーザの名前                                                         | 任意のユーザ名を設定                                                                                                                              |                                                                                                                             |
| ユーザコード                 | 対象ユーザのユーザコード                                             | 任意のユーザコードを設定                                                                                                                          |                                                                                                                             |
| パスワード                   | システムにログインするためのパスワード                               | 新規登録時のみ表示。任意の文字列。                                                                                                                | 文字数や必須文字種などの条件は「[Security.json](../../setup/parameters/security-json.md)のPasswordPolicies の設定に従います |
| 再入力                       | パスワード確認用                                                     | 新規登録時のみ表示。パスワードに設定した文字列を再入力                                                                                            |                                                                                                                             |
| 言語                         | ログインユーザが使用する言語                                         | 任意の言語を設定                                                                                                                                  |                                                                                                                             |
| タイムゾーン                 | システム時刻を計算するために使用されるタイムゾーン                   | 任意のタイムゾーンを設定                                                                                                                          |                                                                                                                             |
| 組織                         | ユーザの所属する組織                                                 | 任意の組織を設定                                                                                                                                  |                                                                                                                             |
| 管理者                       | 上長や承認者など対象ユーザに関連するユーザ                           | 任意のユーザを設定。複数選択不可                                                                                                                  |                                                                                                                             |
| テーマ                       | 画面のユーザインターフェース                                         | 任意のテーマを設定                                                                                                                                |                                                                                                                             |
| 説明                         | 対象ユーザに対する説明                                               | 任意の内容を記載                                                                                                                                  |                                                                                                                             |
| 最終ログイン日時             | 対象ユーザが最終ログインした日時                                     | 編集不可                                                                                                                                          |                                                                                                                             |
| パスワード有効期限           | 対象ユーザのログインパスワードの有効期限                             | 任意の日時を設定                                                                                                                                  |                                                                                                                             |
| パスワード変更日時           | 対象ユーザのログインパスワードを変更した日時                         | 編集不可                                                                                                                                          |                                                                                                                             |
| ログイン回数                 | 対象ユーザがログインした回数                                         | 編集不可                                                                                                                                          |                                                                                                                             |
| ログイン失敗回数             | 対象ユーザがログインを失敗した回数                                   | 編集不可                                                                                                                                          |                                                                                                                             |
| テナント管理者               | システム管理者としての権限                                           | チェックを付けた場合テナント管理者                                                                                                                |                                                                                                                             |
| サイトトップへの作成を許可   | サイトトップへの作成許可権限                                         | チェックを付けた場合そのユーザのみサイトトップへの作成を許可                                                                                      | [User.json](../../setup/parameters/user-json.md)のDisableTopSiteCreationがtrueの場合に表示                                  |
| サイトトップからの移動を許可 | サイトトップからの移動許可権限                                       | 、チェックを付けた場合そのユーザのみサイトトップのフォルダやテーブル等の移動を許可                                                                | [User.json](../../setup/parameters/user-json.md)のDisableMovingFromTopSiteがtrueの場合に表示                                |
| グループの管理を許可         | グループの管理許可権限                                               | [User.json](../../setup/parameters/user-json.md)のDisableGroupAdminがtrueの場合に表示され、チェックを付けた場合そのユーザのみグループの管理を許可 | [User.json](../../setup/parameters/user-json.md)のDisableGroupCreationがtrueの場合に表示                                    |
| グループの作成を許可         | グループの作成許可権限                                               | チェックを付けた場合、そのユーザのみグループの作成を許可                                                                                          |                                                                                                                             |
| APIを許可                    | APIの許可権限                                                        | チェックを付けた場合そのユーザのみAPIを許可                                                                                                       | [User.json](../../setup/parameters/user-json.md)のDisableApiがtrueの場合に表示                                              |
| 2段階認証の有効化            | 2段階認証の有効化設定                                                | チェックを付けた場合そのユーザは2段階認証が有効になります。                                                                                       | [Security.json](../../setup/parameters/security-json.md)のSecondaryAuthentication/ModeがDefaultDisableの場合に表示          |
| 2段階認証の無効化            | 2段階認証の無効化設定                                                | チェックを付けた場合そのユーザは2段階認証が無効になります。                                                                                       | [Security.json](../../setup/parameters/security-json.md)のSecondaryAuthentication/ModeがDefaultEnableの場合に表示           |
| 秘密鍵有効                   | TOTP認証の連携有無設定                                               | 認証アプリとの連携を行うと自動的にチェックが付きます。チェックを外すことで認証アプリとの連携を無効化できます。                                    | [Security.json](../../setup/parameters/security-json.md)のSecondaryAuthentication/NotificationTypeがTotpの場合に表示        |
| 無効                         | ユーザのログイン有効化/無効                                          | チェックを付けた場合ログインを無効                                                                                                                |                                                                                                                             |
| ロック                       | ユーザのログイン有効化/無効                                          | ロックカウンターが[Security.json](../../setup/parameters/security-json.md)のLockoutCountで指定した回数を超えた場合に自動で無効化                  |                                                                                                                             |
| ロックカウンター             | 対象ユーザのログイン失敗回数                                         | ログイン失敗時に自動でカウントアップ                                                                                                              |                                                                                                                             |
| ログイン有効期限             | 対象ユーザがログインできる期限                                       | 任意の日付を設定                                                                                                                                  |                                                                                                                             |
| 無効化までの日数             | 最終ログイン日時から設定した日数ログインしなかった場合にログインNG。 | 任意の日数を設定。未入力および0の場合は無効化しない                                                                                               |                                                                                                                             |

## パスワード入力欄のアイコンについて

### パスワードの確認

「パスワード」欄および「再入力」欄右側の"目"のアイコンをクリックすると入力中のパスワードを確認できます。もう一度クリックすると伏字状態に戻ります。

![「パスワード」欄と「再入力」欄。右側に"目"のアイコンがある](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/5a73e2490fa74b1cb21e12e574a3a5c5.png)

### パスワードの自動生成

1.  「パスワード」欄右側の"鍵"のアイコンをクリックする。
1.  「パスワード」欄と「再入力」欄にランダムに生成されたパスワードが入力される。クリックする度に新しいパスワードが生成される。

    ![パスワードが自動生成された「パスワード」欄と「再入力」欄](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/6f11247e8c1149338e5ca3e196f6983d.png)

-   パスワードは[Security.json](../../setup/parameters/security-json.md)の「PasswordPolicies」で指定したポリシーに従って生成されます。
-   "鍵"アイコンは[Security.json](../../setup/parameters/security-json.md)の「PasswordGenerator」がtrueの場合に表示します。

## 対応バージョン

| 対応バージョン | 内容                                                                         |
| :------------- | :--------------------------------------------------------------------------- |
| 1.4.13.0 以降  | 管理者項目を追加<br>ログイン有効期限項目を追加<br>無効化までの日数項目を追加 |

## 関連情報

-   [プリザンターとActive Directoryを連携する ― AD連携](../../setup/additional/authn-authz/active-directory.md)
-   [SAML認証を利用する](../../setup/additional/authn-authz/saml.md)
-   [ユーザ管理機能：パスワードリセット](user-password-reset.md)
-   [FAQ：Pleasanter.netのユーザ管理で利用可能な機能について](../../FAQ/pleasanter.net/faq-pleasanter-net-user.md)
-   [ユーザ管理機能：テナント管理者の設定](user-management-tenant-manager.md)
-   [ユーザ管理機能](index.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
-   [パラメータ設定：User.json](../../setup/parameters/user-json.md)
