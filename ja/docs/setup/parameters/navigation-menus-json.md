---
title: NavigationMenus.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: navigation-menus-json
translationKey: navigation-menus-json
shortname: NavigationMenus.json
created: 2021-04-09
updated: 2024-10-31
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 制限事項

1. [ユーザインターフェースのテーマ](../../managers-guide/user-administration/user-management-theme.md)で第2世代ユーザインターフェースのテーマの場合は、「NavigationMenus.json」または[拡張ナビゲーションメニュー](../../developers-guide/extended-features/extended-navigationmenus.md)による子メニューの追加は最大3階層まで設定できます。
1. [ユーザインターフェースのテーマ](../../managers-guide/user-administration/user-management-theme.md)で第2世代ユーザインターフェースのテーマの場合は、「NavigationMenus.json」または[拡張ナビゲーションメニュー](../../developers-guide/extended-features/extended-navigationmenus.md)によるIconの指定には対応していません。

## 設定値

本パラメータファイルの設定値は下記の通りです。

| パラメータ名      | 設定例                      | 説明                                                                                                                                                                                                                                                                                                                                                                                                |
| :---------------- | :-------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ContainerId       | NewMenuContainer      | 変更不可 (リスト全体のid属性の値を指定します。)                                                                                                                                                                                                                                             |
| MenuId            | SettingsMenu             | 変更不可 (メニューのid属性の値を指定します。)                                                                                                                                                                                                                                                                                                                                                |
| Id                | SettingsMenu             | 変更不可 (メニューのid属性の値を指定します。)                                                                                                                                                                                                                                       |
| Name              | New                      | メニューの表示名を指定します。Implem.Pleasanter\App_Data\Displays 配下にあるファイル名(拡張子省略)、若しくは任意の文字列を設定することが可能です。                                                                                                                                                            |
| Icon              | ui-icon ui-icon-plus     | メニューのアイコンを指定します。[ユーザインターフェースのテーマ](../../managers-guide/user-administration/user-management-theme.md)で第1世代ユーザインターフェースのテーマの場合のみ有効となります。jQuery UIで公開されているアイコンを設定することが可能です。(参考: https://api.jqueryui.com/theming/icons/)                                                                                                                                                                                                                                                                                                                                                                              |
| Url               | "https://pleasanter.net" | リンク先のURLを指定します。                                                                                                                                                                                                                                                                                                                                                                         |
| Target            | \_blank                  | メニュークリック時のターゲット属性を指定します。例の場合、遷移先の画面を別タブで表示します。                                                                                                                                                                                                                                                                                                                                                            |
| LinkParams        | [  "Users", "Logout" ]             | リンク先をパラメータ形式で指定します。  例の場合、「https://{サーバー名}/users/logout」に遷移します。                                                                                                                                                                                                                                                                                                                                                            |
| Function          | Export                   | 変更不可 (メニュークリック時の処理がある場合に使用します。)                                                                                                                                                                                                                                                                                                                                                                                            |
| Controllers       | [ "items", "users" ]              | プリザンターのコントローラータイプを指定します。指定されたコントローラータイプの画面以外は、メニューが非表示になります。|
| ReferenceTypes    | [ "Users" ]              | プリザンターのリファレンスタイプを指定します。指定されたリファレンスタイプの画面以外は、メニューが非表示になります。 ※1                                                                                                                                                                                                                                                                                                                                                                                                    |
| Actions           | [ "new" ]                | プリザンターのアクションタイプを指定します。指定されたアクションタイプの画面以外は、メニューが非表示になります。                                                                                                                                                                                                                                                                                                                                                                                             |
| ChildMenus| "****"                           | 子メニューの設定を記載します。                                                                                                                                                                                                                                                                                                                                                                                      |
| Disabled| true                           | メニューを無効化します。                                                      |

※1 "-***"と指定する場合、指定した値を除いてメニュー表示の制御を行います。
(例) Controllersに["-items"]を指定する場合、コントローラータイプが"items"の画面はメニューが非表示になり、"items"以外の画面はメニューが表示されます。

## ChildMenuSettings記載例

ChildMenusのパラメータに、メニューと同様の設定を指定することが可能です。

##### JSON

```
[
    {
        "ContainerId": "HelpMenuContainer",
        "MenuId": "HelpMenu",
        "Name": "HelpMenu",
        "Icon": "ui-icon ui-icon-help",
        "ChildMenus": [
            {
                "MenuId": "HelpMenu_UserManual",
                "Name": "UserManual",
                "Icon": "ui-icon ui-icon-help",
                "Url": "https://pleasanter.org/manual",
                "Target": "_blank"
            }
        ]
    }
]
```
