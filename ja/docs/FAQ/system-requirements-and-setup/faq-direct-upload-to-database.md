---
title: ロードバランサのバックエンドにプリザンターを導入したサーバが複数台ある環境で添付ファイルを正常にアップロード、登録することができない
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-direct-upload-to-database
translationKey: faq-direct-upload-to-database
shortname: ''
created: 2024-05-08
updated: 2024-05-14
---

## 回答

[BinaryStorage.json](../../setup/parameters/binary-storage-json.md)のTemporaryBinaryStorageProviderに"Rds"を指定してください

---

## 概要

### BinaryStorage.jsonのTemporaryBinaryStorageProviderに 既定値(null) を指定している場合

下図のようにロードバランサ(LB)のバックエンドにプリザンターを導入したサーバが複数台(WEB#1,WEB#2)ある環境で、[添付ファイル項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)にファイルをアップロードしようとすると、ロードバランサによってリクエストが振り分けられるため、正常にアップロードや登録ができないケースがあります。

![ロードバランサの配下にWEBサーバが2台ある構成の図](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/ed501215fb8b464fb222f3f34100c9a1.png)

TemporaryBinaryStorageProviderを null を指定している場合、WEBサーバの一時フォルダ(App_Data/Temp)に、アップロードしたファイルが保存され、後続の処理(作成や更新)を行うタイミングで、その一時フォルダ配下にある対象ファイルを読み込んで、そのバイナリデータをデータベース(Implem.Pleasanter)のBinariesテーブルへ登録します。

そのため、ロードバランサによって、アップロードのリクエストを受け取るWEBサーバと、後続処理のリクエストを受け取るWEBサーバが異なるケースや、分割して送られたデータ(サイズが大きいファイルは分割する)を片方のWEBサーバで全て受け取れないケースのような状況になると、正常にアップロードや登録ができません。

### BinaryStorage.jsonのTemporaryBinaryStorageProviderに "Rds" を指定している場合

上記の回答に記載の通り、TemporaryBinaryStorageProviderに "Rds" を指定することで、下図の赤線のようにデータベース(Implem.Pleasanter)へデータを直接登録することができるようになります。

![データベースへ直接登録される経路を赤線で示した構成の図](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/09840d0f824f43969f0c2439b4477b7b.png)

Binariesテーブルに登録するレコードのBinaryTypeカラムは、アップロードした時点では "Temporary" で、後続処理を行ったタイミングでは "Attachments" となります。

## 設定手順

下記手順は上図のようにプリザンターを導入するサーバが2台(WEB#1,2)あることを前提としています。

1. WEB#1にログインします。
2. App_Data/Parameters/BinaryStorage.jsonを開きます。
3. ファイル内の各パラメータを以下のように設定して保存します。パラメータの詳細につきましては、 [パラメータ設定：BinaryStorage.json](../../setup/parameters/binary-storage-json.md) を参照してください。
    - Provider："Rds"
    - UseStorageSelect：false
    - TemporaryBinaryStorageProvider："Rds"
4. プリザンターを再起動します。
5. WEB#2も同様に手順1~4を実施します。

## 関連情報

-   [パラメータ設定：BinaryStorage.json](../../setup/parameters/binary-storage-json.md)
-   [テーブルの管理：項目：添付ファイル](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
