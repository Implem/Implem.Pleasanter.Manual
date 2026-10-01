---
title: SitePackage.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: site-package-json
translationKey: site-package-json
shortname: SitePackage.json
created: 2021-04-14
updated: 2024-12-12
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Import|true|サイトパッケージのインポート機能が有効化されます。|
|Export|true|サイトパッケージのエクスポート機能が有効化されます。|
|ExportLimit|0|サイトパッケージのエクスポート時に「データを含める」で出力対象となったレコード数の上限を指定します。0の場合には無制限となります。|
|IncludeDataOnImport|On|サイトパッケージのインポート時に「データを含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合インポートされません。|
|IncludeSitePermissionOnImport|On|サイトパッケージのインポート時に「サイトのアクセス制御を含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合インポートされません。|
|IncludeRecordPermissionOnImport|On|サイトパッケージのインポート時に「レコードのアクセス制御を含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合インポートされません。|
|IncludeColumnPermissionOnImport|On|サイトパッケージのインポート時に「項目のアクセス制御を含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合インポートされません。|
|IncludeNotificationsOnImport|On|サイトパッケージのインポート時に「通知を含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合インポートされません。|
|IncludeRemindersOnImport|On|サイトパッケージのインポート時に「リマインダーを含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合インポートされません。|
|IncludeDataOnExport|On|サイトパッケージのエクスポート時に「データを含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合エクスポートされません。|
|UseIndentOptionOnExport|On|サイトパッケージのエクスポート時に「インデント機能を使う」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合エクスポートされません。|
|IncludeSitePermissionOnExport|On|サイトパッケージのエクスポート時に「サイトのアクセス制御を含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合エクスポートされません。|
|IncludeRecordPermissionOnExport|On|サイトパッケージのエクスポート時に「レコードのアクセス制御を含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合エクスポートされません。|
|IncludeColumnPermissionOnExport|On|サイトパッケージのエクスポート時に「項目のアクセス制御を含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合エクスポートされません。|
|IncludeNotificationsOnExport|On|サイトパッケージのエクスポート時に「通知を含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合エクスポートされません。|
|IncludeRemindersOnExport|On|サイトパッケージのエクスポート時に「リマインダーを含める」のデフォルト値を指定します。"On"のときチェックオン、"Off"のときチェックオフ、”Disabled”のとき設定項目を非表示にします。Disabled指定した場合エクスポートされません。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.18.0 以降|IncludeDataOnImportの追加<br>IncludeSitePermissionOnImportの追加<br>IncludeRecordPermissionOnImportの追加<br>IncludeColumnPermissionOnImportの追加<br>IncludeNotificationsOnImportの追加<br>IncludeRemindersOnImportの追加<br>IncludeDataOnExportの追加<br>UseIndentOptionOnExportの追加<br>IncludeSitePermissionOnExportの追加<br>IncludeRecordPermissionOnExportの追加<br>IncludeColumnPermissionOnExportの追加<br>IncludeNotificationsOnExportの追加<br>IncludeRemindersOnExportの追加|
