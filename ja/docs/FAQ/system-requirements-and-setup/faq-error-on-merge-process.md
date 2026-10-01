---
title: バージョンアップ時のマージ処理中に「Object reference not set to an instance of an object」というエラーが表示される
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-error-on-merge-process
translationKey: faq-error-on-merge-process
shortname: ''
created: 2026-03-24
updated: 2026-03-30
---

## 回答

設定ファイル[General.json](../../setup/parameters/general.json.md)と[NavigationMenus.json](../../setup/parameters/navigation-menus-json.md)の[パラメータを手動で再設定](faq-merge-parameters.md)後、Code Definerまたはインストーラを再度実行してください。

---

## 概要

ver.1.4.17.0にバージョンアップ時に、インストーラおよびCodeDefinerのマージ機能を利用すると、下記の設定ファイルのパラメータが初期値に設定されます。値を変更している場合には、[パラメータを手動で再設定](faq-merge-parameters.md)してください。

### [General.json](../../setup/parameters/general.json.md)

| パラメータ名                    |
| :------------------------------ |
| HtmlApplicationBuildingGuideUrl |
| HtmlUserManualUrl               |
| HtmlSupportUrl                  |
| HtmlTrialLicenseUrl             |
| HtmlEnterpriseEditionUrl        |
| HtmlCasesUrl                    |

### [NavigationMenus.json](../../setup/parameters/navigation-menus-json.md)

下記MenuIdの**Urlプロパティ**

| パラメータ名                  |
| :---------------------------- |
| HelpMenuContainer             |
| HelpMenu_UserManual           |
| HelpMenu_AnnualSupportService |
| HelpMenu_EnterpriseEdition    |
| HelpMenu_Blog                 |
| HelpMenu_Contact              |
| HelpMenu_Portal               |

手動による再設定は一度実施すればよく、次回以降のバージョンアップでは手動による再設定は不要です。

なお、ナビゲーションメニューをカスタマイズしたい場合は、[拡張ナビゲーションメニュー](../../developers-guide/extended-features/extended-navigationmenus.md)を利用してください。拡張ナビゲーションメニューは1.4.4.0以降で利用可能です。

## 関連情報

-   [パラメータ設定：General.json](../../setup/parameters/general.json.md)
-   [パラメータ設定：NavigationMenus.json](../../setup/parameters/navigation-menus-json.md)
-   [FAQ:パラメータを手動で再設定する手順を知りたい](faq-merge-parameters.md)
-   [開発者ガイド：拡張機能：拡張ナビゲーションメニュー](../../developers-guide/extended-features/extended-navigationmenus.md)
