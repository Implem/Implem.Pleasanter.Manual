---
title: 拡張ナビゲーションメニュー
category: 拡張機能
order: '0'
status: ''
parts: ''
urlstring: extended-navigationmenus
translationKey: extended-navigationmenus
shortname: 拡張ナビゲーションメニュー
created: 2021-08-20
updated: 2026-08-17
---

## 概要

ナビゲーションメニューへのメニューの追加、削除等を行うための拡張機能です。

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](../../setup/parameters/parameter-edit.md)を確認してください。

## 制限事項

1.  拡張ナビゲーションメニューのJSONファイルを更新した後は「プリザンターを再起動」するまで反映しません。
1.  [ユーザインターフェースのテーマ](../../managers-guide/user-administration/user-management-theme.md)で第2世代ユーザインターフェースのテーマの場合は、[NavigationMenus.json](../../setup/parameters/navigation-menus-json.md)または「拡張ナビゲーションメニュー」による子メニューの追加は最大3階層まで設定できます。
1.  [ユーザインターフェースのテーマ](../../managers-guide/user-administration/user-management-theme.md)で第2世代ユーザインターフェースのテーマの場合は、[NavigationMenus.json](../../setup/parameters/navigation-menus-json.md)または「拡張ナビゲーションメニュー」によるIconの指定には対応していません。

## 設定方法

.\Pleasanter\App_Data\Parameters\ExtendedNavigationMenus\配下に以下の内容を含むJSONファイルを作成し、「アプリケーションを再起動」してください。ファイルの拡張子は必ずjsonにしてください。ExtendedNavigationMenus配下はフォルダで階層化することが可能です。この場合、配下の全てのJSONファイルが設定ファイルとして読み込まれます。

## パラメータリスト

JSONファイルに指定するパラメータは以下の通りです。

| パラメータ名    | 設定例                                          | 説明                                                                                                                                        |
| :-------------- | :---------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------ |
| Description     | "この拡張ナビゲーションメニューは…を表示します" | 拡張ナビゲーションメニューの説明。動作には影響しません。                                                                                    |
| Disabled        | false                                           | trueの場合は無効化され動作しません。                                                                                                        |
| DeptIdList      | [1,2,3]                                         | 対象となる組織IDを配列形式で指定します。指定しない場合には省略可能です。                                                                    |
| GroupIdList     | [1,2,3]                                         | 対象となるグループIDを配列形式で指定します。指定しない場合には省略可能です。                                                                |
| UserIdList      | [1,2,3]                                         | 対象となるユーザIDを配列形式で指定します。指定しない場合には省略可能です。                                                                  |
| SiteIdList      | [1,2,3]                                         | 対象となるサイトのサイトIDを配列形式で指定します。指定しない場合には省略可能です。                                                          |
| IdList          | [1,2,3]                                         | 対象となるレコードのIDを配列形式で指定します。指定しない場合には省略可能です。                                                              |
| TargetId        | "NewMenu"                                       | Actionで指定した操作をする時の対象となるIDを指定します。                                                                                    |
| Action          | "Append"                                        | メニューの追加、削除等の操作を指定します。                                                                                                  |
| NavigationMenus | [{…},{…},…]                                     | 拡張するメニューの定義を指定します。パラメータ設定の[NavigationMenus.json](../../setup/parameters/navigation-menus-json.md)を参照ください。 |

## TargetId一覧

|              ナビゲーションメニュー              | TargetId     |
| :----------------------------------------------: | :----------- |
| ![TargetIdがNewMenuのナビゲーションメニュー](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/80130ca166c64c77b145eb804c6abe4a.png) | NewMenu      |
| ![TargetIdがViewModeMenuのナビゲーションメニュー](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/25d85d8927204dca8a7ffc4907677e6c.png) | ViewModeMenu |
| ![TargetIdがSettingsMenuのナビゲーションメニュー](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/853553d4d10b4bdab82a7295844304e0.png) | SettingsMenu |
| ![TargetIdがHelpMenuのナビゲーションメニュー](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/f4e14889028643a6861dd7ecb2dd227f.png) | HelpMenu     |
| ![TargetIdがAccountMenuのナビゲーションメニュー](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/f8679c6fbac24c5994c80e2bc1116114.png) | AccountMenu  |

## Action一覧

Actionに指定できる操作についての一覧です。

| 変数       | 説明                                                         |
| :--------- | :----------------------------------------------------------- |
| Prepend    | TargetIdで指定したIDのメニューの前にメニューを追加します。   |
| Append     | TargetIdで指定したIDのメニューの後ろにメニューを追加します。 |
| Remove     | TargetIdで指定したIDのメニューを削除します。                 |
| Replace    | TargetIdで指定したIDのメニューを置換します。                 |
| ReplaceAll | メニューをすべて置換します。                                 |

![拡張ナビゲーションメニューAction一覧](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/20f53a0c662443058e278d2ba20357c4.png)

## サンプルコード

<details markdown="1">

<summary style="font-weightbold; color:#1d3994">❶ 新規作成（NewMenu）の前（上）に追加</summary>

```json linenums="1"
{
    "TargetId": "NewMenu",
    "Action": "Prepend",
    "NavigationMenus": [
        {
            "ContainerId": "ProductManagementContainer",
            "MenuId": "ProductManagement",
            "Name": "商品管理",
            "Icon": "ui-icon ui-icon-gear",
            "ChildMenus": [
                {
                    "Name": "食品",
                    "MenuId": "Food",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "569", "Index" ]
                },
                {
                    "Name": "飲料",
                    "MenuId": "Beverage",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "570", "Index" ]
                },
                {
                    "Name": "日用品",
                    "MenuId": "DailyEssentials",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "571", "Index" ]
                }
            ]
        }
    ]
}
```

##### 表示結果

青枠がTargetIdの指すナビゲーションメニュー、赤枠が置換後のナビゲーションメニューです。

![NewMenuの前にメニューを追加した表示結果](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/fc565090d43f41abbff3de5360b8a8c4.png)
</details>

<details markdown="1">

<summary style="font-weightbold; color:#1d3994">➋ 新規作成（NewMenu）の後（下）に追加</summary>

```json
{
    "TargetId": "NewMenu",
    "Action": "Append",
    "NavigationMenus": [
        {
            "ContainerId": "ProductManagementContainer",
            "MenuId": "ProductManagement",
            "Name": "商品管理",
            "Icon": "ui-icon ui-icon-gear",
            "ChildMenus": [
                {
                    "Name": "食品",
                    "MenuId": "Food",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "569", "Index" ]
                },
                {
                    "Name": "飲料",
                    "MenuId": "Beverage",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "570", "Index" ]
                },
                {
                    "Name": "日用品",
                    "MenuId": "DailyEssentials",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "571", "Index" ]
                }
            ]
        }
    ]
}
```

##### 表示結果

青枠がTargetIdの指すナビゲーションメニュー、赤枠が置換後のナビゲーションメニューです。

![NewMenuの後ろにメニューを追加した表示結果](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/fad20509a13740fbb078fc2b5ca1e545.png)

</details>

<details markdown="1">

<summary style="font-weightbold; color:#1d3994">➌ ヘルプメニュー（HelpMenu）を削除（Remove）</summary>

``` json
{
    "TargetId": "HelpMenu",
    "Action": "Remove"
}
```

##### 表示結果

青枠がTargetIdの指すナビゲーションメニューです。変更後、青枠部分がナビゲーションメニューからなくなります。

![HelpMenuを削除した表示結果](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/eeee60a07d214f039964e72ff6518ba6.png)

</details>

<details markdown="1">

<summary style="font-weightbold; color:#1d3994">❹ ヘルプメニュー（HelpMenu）を置換（Replace）</summary>

```json
{
    "TargetId": "HelpMenu",
    "Action": "Replace",
    "NavigationMenus": [
        {
            "ContainerId": "ProductManagementContainer",
            "MenuId": "ProductManagement",
            "Name": "商品管理",
            "Icon": "ui-icon ui-icon-gear",
            "ChildMenus": [
                {
                    "Name": "食品",
                    "MenuId": "Food",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "569", "Index" ]
                },
                {
                    "Name": "飲料",
                    "MenuId": "Beverage",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "570", "Index" ]
                },
                {
                    "Name": "日用品",
                    "MenuId": "DailyEssentials",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "571", "Index" ]
                }
            ]
        }
    ]
}
```

##### 表示結果

青枠がTargetIdの指すナビゲーションメニュー、赤枠が置換後のナビゲーションメニューです。

![HelpMenuを置換した表示結果](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/73a65390a67a424aa9806874f2eec27e.png)

</details>

<details markdown="1">

<summary style="font-weightbold; color:#1d3994">❺ 全メニューを置換（ReplaceAll）</summary>

``` json
{
    "TargetId": "HelpMenu",
    "Action": "ReplaceAll",
    "NavigationMenus": [
        {
            "ContainerId": "ProductManagementContainer",
            "MenuId": "ProductManagement",
            "Name": "商品管理",
            "Icon": "ui-icon ui-icon-gear",
            "ChildMenus": [
                {
                    "Name": "食品",
                    "MenuId": "Food",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "569", "Index" ]
                },
                {
                    "Name": "飲料",
                    "MenuId": "Beverage",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "570", "Index" ]
                },
                {
                    "Name": "日用品",
                    "MenuId": "DailyEssentials",
                    "Icon": "ui-icon ui-icon-triangle-1-e",
                    "LinkParams": [ "Items", "571", "Index" ]
                }
            ]
        }
    ]
}
```

##### 表示結果

青枠がReplaceAllの対象となるナビゲーションメニュー、赤枠が置換後のナビゲーションメニューです。

![メニューをすべて置換した表示結果](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/61c7ce103f484d3f93bee651f07fcedc.png)

</details>

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](../../setup/parameters/parameter-edit.md)
-   [ユーザ管理機能：ユーザインターフェースのテーマをカスタマイズ](../../managers-guide/user-administration/user-management-theme.md)
-   [パラメータ設定：NavigationMenus.json](../../setup/parameters/navigation-menus-json.md)
