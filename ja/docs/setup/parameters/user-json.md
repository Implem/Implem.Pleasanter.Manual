---
title: User.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: user-json
translationKey: user-json
shortname: User.json
created: 2021-04-05
updated: 2024-12-12
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

-   本パラメータファイルの設定値は下記の通りです。

| パラメータ名             | 設定例     | 説明                                                                                                                                                                                                                                                                                                                                                              |
| :----------------------- | :--------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DisableTopSiteCreation   | false      | true<br>[トップ画面](../../users-guide/hands-on/basics/basic-operations-description.md)での[サイト](../../users-guide/site/index.md)の作成を制限します。[ユーザの管理](../../managers-guide/user-administration/index.md)画面で[サイトトップへの作成を許可](../../FAQ/top-screen-site-menu/faq-disable-top-site-creation.md)のチェックをオンにしたユーザのみがトップ画面にサイトを作成できます。<br><br>false<br>すべてのユーザがトップ画面にサイトを作成できます。<br><br><!-- meta version="1.1.16.0" --> |
| DisableMovingFromTopSite | false      | true<br>トップ画面から下位フォルダへのサイトの移動を制限します。[ユーザの管理](../../managers-guide/user-administration/index.md)画面で[サイトトップからの移動を許可](../../managers-guide/user-administration/user-new-edit.md)のチェックをオンにしたユーザのみがトップ画面のサイトを下位フォルダへ移動できます。<br><br>false<br>すべてのユーザがトップ画面のサイトを下位フォルダへ移動できます。                                                                         |
| DisableGroupAdmin        | false      | ユーザにグループの管理を許可しない場合にはtrueを設定します。このパラメータをtrueにした場合、ユーザの編集画面で「グループの管理を許可」にチェックを入れたユーザのみがグループの管理を行えます。<br><br><!-- meta version="1.1.16.0" -->                                                                                                                            |
| DisableGroupCreation     | false      | ユーザにグループの作成を許可しない場合にはtrueを設定します。このパラメータをtrueにした場合、ユーザの編集画面で「グループの作成を許可」にチェックを入れたユーザのみがグループの作成を行えます。<br><br><!-- meta version="1.2.14.0" -->                                                                                                                            |
| DisableApi               | false      | ユーザにAPIの使用を許可しない場合にはtrueを設定します。このパラメータをtrueにした場合、ユーザの編集画面で「APIを許可」にチェックを入れたユーザのみがAPIを使用できます。                                                                                                                                                                                           |
| SelectorToolTip          | "LoginId"  | グループの管理やサイトのアクセス制御の権限設定で、ユーザ選択時のツールチップに表示する内容を設定します。"LoginId"または"MailAddress"を設定できます。                                                                                                                                                                                                            |
| Theme                    | "cerulean" | [ユーザインターフェースのテーマ](../../managers-guide/user-administration/user-management-theme.md)を指定します。<br><br><!-- default="cerulean"  -->                                                                                                                                                                                                                                                      |

## 対応バージョン

| 対応バージョン | 内容                                                    |
| :------------- | :------------------------------------------------------ |
| 1.1.16.0以降   | DisableTopSiteCreationを追加<br>DisableGroupAdminを追加 |
| 1.2.14.0以降   | DisableGroupCreationを追加                              |
| 1.4.3.0以降    | Themeを「cerulean」に変更                               |

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [ユーザ管理機能：ユーザインターフェースのテーマをカスタマイズ](../../managers-guide/user-administration/user-management-theme.md)
