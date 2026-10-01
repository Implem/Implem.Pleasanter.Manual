---
title: プリザンターでKVSを利用する
category: 追加設定：パフォーマンス
order: '100'
status: ''
parts: ''
urlstring: kvs
translationKey: kvs
shortname: ''
created: 2024-10-29
updated: 2024-12-10
---

## 概要

セッションデータの保持に[KVS](../../installation/install-database/kvs-install.md)を利用するための設定方法です。
[KVS](../../installation/install-database/kvs-install.md)を利用することで、多数のユーザでの同時アクセスにおいて、画面の表示速度などのパフォーマンスが向上する可能性があります。

## 前提条件

[KVS](../../installation/install-database/kvs-install.md)をあらかじめインストールしてください。[KVS](../../installation/install-database/kvs-install.md)のインストール方法については下記を参照してください。
「KVSのインストール」

## 操作手順

1. [Session.json](../../parameters/session-json.md)のUseKeyValueStoreをtrueに変更してください。
```
{
    "RetentionPeriod": 1440,
    "UseKeyValueStore": true
}
```

1. [Kvs.json](../../parameters/kvs-json.md)のConnectionStringForSessionを設定してください。
```
{
    "ConnectionStringForSession": "<キャッシュのホスト名>:<キャッシュのポート番号>,password=<キャッシュのパスワード>,ssl=True,abortConnect=False"
}
```

## 関連情報

-   [KVSのインストール](../../installation/install-database/kvs-install.md)
-   [パラメータ設定：Session.json](../../parameters/session-json.md)
-   [パラメータ設定：Kvs.json](../../parameters/kvs-json.md)