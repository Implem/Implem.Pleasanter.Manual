---
title: ver.1.4.17.0以降でマージ機能を利用する際の注意事項
category: バージョンアップ(インストーラ)
order: '400'
status: ''
parts: ''
urlstring: version-up-ver1.4.17.0-caution
translationKey: version-up-ver1.4.17.0-caution
shortname: ver.1.4.17.0以降でマージ機能を利用する際の注意事項
created: 2025-06-10
updated: 2026-01-13
---

## 概要

**ver.1.4.17.0以降へのバージョンアップ時に、[インストーラ](../../installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)および[CodeDefiner](../../codedefiner/codedefiner-command.md)のマージ機能を利用すると、下記のパラメータファイルのパラメータが初期値に設定されます。**値を変更している場合には、再度手動での設定をお願いいたします。手動による再設定は一度実施すればよく、次回以降のバージョンアップでは手動による再設定は不要です。

## [General.json](../../parameters/general.json.md)  

|パラメータ名|
|:--|
|HtmlApplicationBuildingGuideUrl|
|HtmlUserManualUrl|
|HtmlSupportUrl|
|HtmlTrialLicenseUrl|
|HtmlEnterpriseEditionUrl|
|HtmlCasesUrl|

## [NavigationMenus.json](../../parameters/navigation-menus-json.md)  

下記MenuIdの**Urlプロパティ**

|パラメータ名|
|:--|
|HelpMenuContainer|
|HelpMenu_UserManual|
|HelpMenu_AnnualSupportService|
|HelpMenu_EnterpriseEdition|
|HelpMenu_Blog|
|HelpMenu_Contact|
|HelpMenu_Portal|

## 関連情報

-   [インストーラでプリザンターをAlmaLinuxにインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)
-   [CodeDefinerのコマンド一覧](../../codedefiner/codedefiner-command.md)
-   [パラメータ設定：General.json](../../parameters/general.json.md)
-   [パラメータ設定：NavigationMenus.json](../../parameters/navigation-menus-json.md)