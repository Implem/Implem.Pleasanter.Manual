---
title: パラメータのマージ機能について
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-codedefiner-parameters-merge
translationKey: faq-codedefiner-parameters-merge
shortname: ''
created: 2025-05-21
updated: 2025-05-29
---

## 回答

旧資源のParameters配下のサブフォルダおよびファイルを新資源にコピーし、ParametersPatch.zip内のパッチファイルを元に、追加されたパラメータおよび削除されたパラメータを適用します。

---

## 概要

下記CodeDefinerのmergeコマンドを実行することで、旧資源 **C:\web\pleasanter_bk\Implem.Pleasanter\App_Data\Parameters** を新資源 **C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters** にコピーします。  
その後、ParametersPatch.zip内のパッチファイルを元に、旧資源のバージョンから新資源のバージョンまでに追加および削除されたパラメータを適用します。

```
dotnet Implem.CodeDefiner.dll merge /b C:\web\pleasanter_bk /i C:\web\pleasanter
```

C:\web\pleasanter_bk\Implem.Pleasanter\App_Data\Parameters\配下にある以下サブフォルダ内の拡張機能で設定したファイルも新資源にコピーされます。

|サブフォルダ名|拡張機能名|備考|
|:---|:---|:---|
|CustomDefinitions|[拡張項目](../../developers-guide/extended-features/extended-column.md)|組織、グループ、ユーザに項目を追加した際に生成されるフォルダ|
|ExtendedFields|[拡張フィールド](../../developers-guide/extended-features/extended-fields.md)||
|ExtendedHtmls|[拡張HTML](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)||
|ExtendedNavigationMenus|[拡張ナビゲーションメニュー](../../developers-guide/extended-features/extended-navigationmenus.md)||
|ExtendedScripts|[拡張スクリプト](../../developers-guide/extended-features/extended-script.md)||
|ExtendedServerScripts|[拡張サーバスクリプト](../../developers-guide/extended-features/extended-server-script.md)||
|ExtendedSqls|[拡張SQL](../../developers-guide/extended-features/extended-sql/index.md)||
|ExtendedStyles|[拡張スタイル](../../developers-guide/extended-features/extended-style.md)||

## 関連情報

[CodeDefinerのコマンド一覧](../../setup/codedefiner/codedefiner-command.md)
[1.4.8.0以降のバージョンアップ手順(Windows)](../../setup/version-up-migration/version-up-manually/version-up-windows-1.4.8.0.md)
[1.4.8.0以降のバージョンアップ手順(Linux)](../../setup/version-up-migration/version-up-manually/version-up-linux-1.4.8.0.md)
[1.4.8.0以降のバージョンアップ手順(Azure App Service)](../../setup/version-up-migration/version-up-manually/version-up-azure-1.4.8.0.md)
-   [開発者ガイド：拡張機能：拡張項目](../../developers-guide/extended-features/extended-column.md)
-   [開発者ガイド：拡張機能：拡張フィールド](../../developers-guide/extended-features/extended-fields.md)
-   [テーブルの管理：エディタ：項目の詳細設定：拡張HTML](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)
-   [開発者ガイド：拡張機能：拡張ナビゲーションメニュー](../../developers-guide/extended-features/extended-navigationmenus.md)
-   [開発者ガイド：拡張機能：拡張スクリプト](../../developers-guide/extended-features/extended-script.md)
-   [開発者ガイド：拡張機能：拡張サーバスクリプト](../../developers-guide/extended-features/extended-server-script.md)
-   [開発者ガイド：拡張機能：拡張SQL](../../developers-guide/extended-features/extended-sql/index.md)
-   [開発者ガイド：拡張機能：拡張スタイル](../../developers-guide/extended-features/extended-style.md)
-   [CodeDefinerのコマンド一覧](../../setup/codedefiner/codedefiner-command.md)