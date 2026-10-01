---
title: BinaryStorage.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: binary-storage-json
translationKey: binary-storage-json
shortname: BinaryStorage.json
created: 2019-04-30
updated: 2026-08-12
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 制限事項

1. TemporaryBinaryStorageProviderに設定可能な"Rds"は、Providerに"Rds"、UseStorageSelectにfalseが設定されている必要があります。※適切な値が設定されていないと正常にファイルを添付することができません。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:----|:--|
|Provider|Rds|添付ファイルや貼付け画像のデータの格納方法を指定します。データベースに格納する場合は"Rds"、ストレージに格納する場合は"Local"、Azure Blob Storageに格納する場合は"AzureBlob"を設定します。|
|AzureBlobStorageAccountUri|"https://storagename.blob.core.<br>windows.net"|ProviderでAzureBlobを指定した場合の格納先となるAzure Blob StorageのストレージアカウントのURIを設定します。接続にはAzureの資格情報（DefaultAzureCredential）を使用します。システム環境変数に登録可能。|
|AzureBlobContainerName|"pleasanter-binaries"|ProviderでAzureBlobを指定した場合の格納先となるBlobコンテナ名を設定します。nullの場合は"pleasanter-binaries"を使用します。コンテナは自動で作成されないため、事前に作成してください。システム環境変数に登録可能。|
|Path|C:\\\\Data |ProviderでLocalを指定した場合の添付ファイルの格納先フォルダを設定します(円記号はエスケープが必要です)。※対象フォルダへのアクセス権をIIS_IUSERSに付与してください。|
|Attachments|true|添付ファイル機能のtrue/falseを指定します。|
|Images|true|説明項目やコメントで画像貼り付け機能のtrue/falseを指定します。画像の貼り付けを有効化するにはAttachmentsとImagesの両方をtrueに設定する必要があります。|
|RestoreLocalFiles| true |ProviderがLocalの場合に、値をtrueにすると添付ファイルを持つレコードを削除してもローカルのファイル削除しません。削除したレコードを復元すると添付ファイルも使用可能となります。Providerが "Local" で値がfalseの場合には、削除されたレコードを復元しても添付ファイルは復元できません。|
|LimitQuantity|30|ファイル数制限の初期値を設定します。|
|MinQuantity|1|ファイル数制限の下限値を設定します。|
|MaxQuantity|100|ファイル数制限の上限値を設定します。|
|LimitSize|50|容量制限(MB)の初期値を設定します。|
|MinSize|1|容量制限(MB)の下限値を設定します。|
|MaxSize|50|容量制限(MB)の上限値を設定します。|
|LimitTotalSize|1024|全容量制限(MB)の初期値を設定します。|
|TotalMinSize|1|全容量制限(MB)の下限値を設定します。|
|TotalMaxSize|1024|全容量制限(MB)の上限値を設定します。|
|LocalFolderLimitSize|3072|ローカルフォルダの容量制限(MB)の初期値を設定します。|
|LocalFolderMinSize|1|ローカルフォルダの容量制限(MB)の下限値を設定します。|
|LocalFolderMaxSize|3072|ローカルフォルダの容量制限(MB)の上限値を設定します。|
|LocalFolderLimitTotalSize|30720|ローカルフォルダの全容量制限(MB)の初期値を設定します。|
|LocalFolderTotalMinSize|1|ローカルフォルダの全容量制限(MB)の下限値を設定します。|
|LocalFolderTotalMaxSize|30720|ローカルフォルダの全容量制限(MB)の上限値を設定します。|
|UseStorageSelect|false|添付項目毎にファイルの[格納先](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-binary-storage-provider.md)を変更する場合はtrueを設定します。|
|DefaultBinaryStorageProvider|"DataBase"|UseStorageSelectがtrueの場合の添付項目の[格納先](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-binary-storage-provider.md)の既定値を設定します。データベースに保存する場合は"DataBase"、ローカルフォルダに保存する場合は"LocalFolder"、サイズにより自動で切り替える場合は"AutoDataBaseOrLocalFolder"を設定します。|
|TemporaryBinaryStorageProvider|"Rds"|アップロードしたファイルを一時フォルダ(App_Data\Temp)配下に保存する場合はnull、直接データベースに保存する場合は"Rds"を指定します。"Rds"を指定する場合は上記の制限事項の内容を確認してください。 ※1|
|ImageLimitSize|10|画像登録時の一辺の最大ピクセル数(px)を設定します。|
|ThumbnailLimitSize|10|サムネイル登録時の一辺の最大ピクセル数(px)を設定します。
|ThumbnailMinSize|100|サムネイルサイズ指定時の一辺の最小ピクセル(px)を設定します。|
|ThumbnailMaxSize|1000|サムネイルサイズ指定時の一辺の最大ピクセル(px)を設定します。|
|BrowserAllowMimeTypes|["application/pdf","image/png"]|[プレビュー表示](../../users-guide/table/record-authoring/edit-records/table-record-attachment-show.md)を許可するファイルのMIMEタイプを配列で設定します。|

※1 TemporaryBinaryStorageProviderの"Rds"は、ロードバランサを経由して、その先にプリザンターが導入されたサーバが複数台ある環境で使用することを想定しています。詳細につきましては下記のFAQを参照してください。  
　[FAQ：ロードバランサのバックエンドにプリザンターを導入したサーバが複数台ある環境で添付ファイルを正常にアップロード、登録することができない | Pleasanter](../../FAQ/system-requirements-and-setup/faq-direct-upload-to-database.md)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.21.0 以降|BrowserAllowMimeTypesを追加|
|1.5.7.0 以降|AzureBlobStorageAccountUri・AzureBlobContainerNameを追加<br>Providerに"AzureBlob"を追加|
