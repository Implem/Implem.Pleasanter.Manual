---
title: IISで100MB以上のファイルをアップロードする場合の事前設定
category: 追加設定：Webサーバ
order: '200'
status: ''
parts: ''
urlstring: iis-large-file-100
translationKey: iis-large-file-100
shortname: アップロード
created: 2019-05-02
updated: 2023-04-12
---

100MB以上のファイルをインポートする場合は以下の手順を行ってください。また、下記の手順に加えて、[こちら](iis-large-file-30.md)の設定も必要です。

## バージョン1.2.0以降

[Service.json](../../parameters/service-json.md)のMaxRequestBodySizeに、インポートを行うファイルの最大サイズを指定してください。

## バージョン0.50以前

1.  C:\inetpub\wwwroot\pleasanterフォルダを開いてください。

    ![inetpub配下のpleasanterフォルダを開いたところ](https://pleasanter.org/files/images/ja/setup/additional/web-server/assets/680df03ef67b4b1b93e717bfd25a89bb.png)

1.  Web.configファイルをメモ帳などで開いてください。

1.  maxRequestLength=""のダブルクォーテーション内にインポートを行うファイルの最大サイズを入力し、ファイルを保存してください。

    ![Web.configのmaxRequestLengthに最大サイズを入力したところ](https://pleasanter.org/files/images/ja/setup/additional/web-server/assets/fd5796c60b714a909b660aceaf079ecd.png)

## 関連情報

-   [IISで30MB以上のファイルをアップロードする場合の事前設定](iis-large-file-30.md)
