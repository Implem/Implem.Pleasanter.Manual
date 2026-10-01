---
title: クラスタ構成で添付ファイルをローカルストレージ格納する設定
category: 追加設定：クラスタ化への備え
order: '0'
status: ''
parts: ''
urlstring: clustering-attachments-store-local-storage
translationKey: clustering-attachments-store-local-storage
shortname: クラスタ構成で添付ファイルをローカルストレージ格納する設定
created: 2026-04-10
updated: 2026-04-10
---

## 前提条件

1. 本ページにおける「クラスタ」はWebサーバのクラスタであり、データベースサーバのクラスタではありません。

## 概要

クラスタ環境下で添付ファイルを正常にアップロード、登録できるようにプリザンターを構成します。

本ページでは、添付ファイルの格納方式として**ローカルストレージ格納**を選択する場合の方法を説明します。データベース格納を選択する場合については、[追加設定：クラスタ化への備え：添付ファイルのアップロード・登録に関する設定](clustering-attachment-item-settings.md)を参照してください。

下図のように、プリザンターを導入するサーバが2台（Webサーバ 1、Webサーバ 2）あることを前提とします。

![Webサーバ2台のクラスタ構成で添付ファイルをローカルストレージへ格納する構成図](https://pleasanter.org/files/images/ja/setup/additional/ready-for-clustering/assets/a0085650d1b84a8bbffc5da4cc154c29.png)

## 操作手順

1. Webサーバ 1にログインしてください。
1. 設定ファイル[BinaryStorage.json](../../parameters/binary-storage-json.md)を開いてください。
1. パラメータ「Provider」の値を"local"に設定し、保存してください。
1. プリザンターを再起動します。
1. Webサーバ 2も同様に、上記の手順1.～4.を実施します。

なお、クラスタ構成でローカルストレージ格納（Local）を選択する場合、複数のWebサーバから共有ストレージへのアクセスが必須です。**<span class="pl-attention">すべてのWebサーバから同一パスで共有ストレージへアクセスできるように設定</span>**してください。

## バックグラウンドサービスのクラスタ対応

バックグラウンドサービスのクラスタ対応については、以下のマニュアルを参照してください。

1. [追加設定：クラスタ化への備え：バックグラウンドサービスを複数インスタンス構成に対応させる](https://pleasanter.org/ja/manual/service-clustering)
1. [追加設定：クラスタ化への備え：添付ファイルのアップロード・登録に関する設定](https://pleasanter.org/ja/manual/clustering-attachment-item-settings)
1. [パラメータ設定：Quartz.json](https://pleasanter.org/ja/manual/quartz-json)

## 関連情報

-   [追加設定：クラスタ化への備え：添付ファイルのアップロード・登録に関する設定](clustering-attachment-item-settings.md)
-   [追加設定：クラスタ化への備え：バックグラウンドサービスを複数インスタンス構成に対応させる](https://pleasanter.org/ja/manual/service-clustering)
-   [追加設定：クラスタ化への備え：添付ファイルのアップロード・登録に関する設定](https://pleasanter.org/ja/manual/clustering-attachment-item-settings)
-   [パラメータ設定：Quartz.json](https://pleasanter.org/ja/manual/quartz-json)