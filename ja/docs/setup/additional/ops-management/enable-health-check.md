---
title: プリザンターのヘルスチェック機能を有効化する
category: 追加設定：運用管理
order: '200'
status: ''
parts: ''
urlstring: enable-health-check
translationKey: enable-health-check
shortname: ヘルスチェック機能
created: 2024-08-30
updated: 2024-09-10
---

## 概要

ヘルスチェック機能を動作させることでプリザンターの稼働状況を確認することができます。

### 設定手順

1. [Security.json](../../parameters/security-json.md)を開き、パラメータ "Enabled" を true に編集し、保存します。
2. プリザンターを再起動します。
3. エンドポイント "**/healthz**" にアクセスし、ヘルスチェック機能が動作することを確認します。

#### 例) http://localhost の場合

アクセスするURLは "http://localhost/healthz" となります。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.8.0 以降|機能追加|

## 関連情報

-   [パラメータ設定：Security.json](../../parameters/security-json.md)
