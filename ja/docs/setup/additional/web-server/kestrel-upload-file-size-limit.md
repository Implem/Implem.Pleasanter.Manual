---
title: Linux環境でインポートやアップロードするファイルサイズの上限値を設定する
category: 追加設定：Webサーバ
order: '300'
status: ''
parts: ''
urlstring: kestrel-upload-file-size-limit
translationKey: kestrel-upload-file-size-limit
shortname: ''
created: 2022-04-05
updated: 2025-03-13
---

## 概要

Linux環境でインポートやアップロードするファイルサイズの上限値を設定します。

## 設定方法

1.  /web/pleasanter/Implem.Pleasanter/を開いてください。
1.  appsettings.jsonに以下の設定を追加してください。MaxRequestBodySizeに指定する数値がインポートやアップロードを行うファイルの最大サイズです。

    ``` json title="appsettings.json" linenums="1"
    "Kestrel": {
        "Limits": {
            "MaxRequestBodySize": 10000000000
        }
    }
    ```

1.  プリザンターを再起動してください。
