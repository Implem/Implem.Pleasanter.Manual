---
title: 添付ファイルのアップロード・登録に関する設定
category: 追加設定：クラスタ化への備え
order: '200'
status: ''
parts: ''
urlstring: clustering-attachment-item-settings
translationKey: clustering-attachment-item-settings
shortname: 添付ファイルのアップロード・登録に関する設定
created: 2025-10-30
updated: 2025-11-11
---

## 前提条件

1. 本ページにおける「クラスタ」はAPサーバのクラスタであり、DBサーバのクラスタではありません。

## 概要

既定の設定を変更することで、添付ファイルを正常にアップロード、登録できるようにプリザンターを構成します。

## 操作手順

下図のように、プリザンターを導入するサーバが2台（WEB#1、WEB#2）あることを前提としています。

1. WEB#1にログインしてください。
1. 設定ファイル[BinaryStorage.json](../../parameters/binary-storage-json.md)を開いてください。
1. ファイル内の各パラメータを以下のように設定して保存してください。各パラメータの詳細は「[パラメータ設定：BinaryStorage.json](../../parameters/binary-storage-json.md)」を参照してください。

    |パラメータ|設定値|
    |:--|:--|
    |Provider|"Rds"|
    |UseStorageSelect|false|
    |TemporaryBinaryStorageProvider|"Rds"|

1. プリザンターを再起動します。
1. WEB#2も同様に手順1.～4.を実施します。

この手順の実施が必要となる背景について、詳しくは以下を参照してください。

## 背景知識

プリザンターを複数ノードでクラスタ構成する際、ロードバランサ（LB）がセッション維持（セッションアフィニティ）を行わないラウンドロビン方式などの場合、ログイン認証や一部のセッション管理に関する動作に問題が発生する可能性があります。            
<span class="pl-attention">安定した動作を確保するため、セッション維持機能を有効にした構成（セッションアフィニティ / スティッキーセッション ）を推奨します。</span>

また、添付ファイルのアップロード処理においても、セッションが途中で切り替わることでファイル登録が正常に完了しない事例が確認されています。

### BinaryStorage.jsonのTemporaryBinaryStorageProviderに既定値（null） を指定している場合

下図のようにロードバランサのバックエンドにプリザンターを導入したサーバが複数台（WEB#1、WEB#2）ある環境で、[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)にファイルをアップロードしようとすると、ロードバランサによってリクエストが振り分けられるため、正常にアップロードや登録ができないケースがあります。

![ロードバランサ配下にWebサーバが2台ある構成で添付ファイルをアップロードする流れの図](https://pleasanter.org/files/images/ja/setup/additional/ready-for-clustering/assets/ed501215fb8b464fb222f3f34100c9a1.png)

TemporaryBinaryStorageProviderにnullを指定している場合、Webサーバの一時フォルダ（App_Data/Temp）に、アップロードしたファイルが保存され、後続の処理（作成や更新）を行うタイミングで、その一時フォルダ配下にある対象ファイルを読み込んで、そのバイナリデータをデータベース（Implem.Pleasanter）のBinariesテーブルへ登録します。

そのため、ロードバランサによって、アップロードのリクエストを受け取るWebサーバと、後続処理のリクエストを受け取るWebサーバが異なるケースや、分割して送られたデータ（サイズが大きいファイルは分割する）を片方のWebサーバで全て受け取れないケースのような状況になると、正常にアップロードや登録ができません。

### BinaryStorage.jsonのTemporaryBinaryStorageProviderに "Rds" を指定している場合

上記の回答に記載の通り、TemporaryBinaryStorageProviderに"Rds"を指定することで、下図の赤線のようにデータベース（Implem.Pleasanter）へデータを直接登録することができるようになります。

![TemporaryBinaryStorageProviderに「Rds」を指定し、データベースへ直接登録する流れの図](https://pleasanter.org/files/images/ja/setup/additional/ready-for-clustering/assets/09840d0f824f43969f0c2439b4477b7b.png)

Binariesテーブルに登録するレコードのBinaryTypeカラムは、アップロードした時点では"Temporary"で、後続処理を行ったタイミングでは"Attachments"となります。

## 関連情報

-   [パラメータ設定：BinaryStorage.json](../../parameters/binary-storage-json.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)