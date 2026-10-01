---
title: MultiTenant.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: multitenant-json
translationKey: multitenant-json
shortname: MultiTenant.json
created: 2026-08-03
updated: 2026-08-12
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/parameters/assets/a6a548443e2d4bf8b98fe36db39a35c8.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/parameters/assets/e92b29e496c24fe88a5471179f18bcc3.svg#only-dark)](https://pleasanter.org/support/)

## 注意事項

1. パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。
1.  DefaultTenantIdの値を正しく設定しないと、誰もログインできなくなる可能性があります。

## 設定値

本パラメータファイルの設定値は下記の通りです。

| パラメータ              | 設定例 | 説明                                                                                                                             |
| ----------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------- |
| DefaultTenantId | 1    | 保護テナントのTenantIdです。本パラメータで指定したテナントは停止、再開、削除APIの対象外（403）となり、バックグラウンド物理削除でもスキップされます。マルチテナントライセンスなしの環境では、このテナントのユーザのみログイン可能です。本パラメータを正しく設定しないと、誰もログインできなくなる可能性があります。 |

## 対応バージョン

| 対応バージョン| 内容|
|---|---|
|1.5.7.0 以降| MultiTenant.jsonを追加|

## 関連情報

-   [パラメータ変更時の確認事項](parameter-edit.md)