---
title: OutputCache.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: outcache-json
translationKey: outcache-json
shortname: ''
created: 2024-06-05
updated: 2025-03-19
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は以下の通りです。

| パラメータ名       | 説明                                                                                   |
| :----------------- | :------------------------------------------------------------------------------------- |
| OutputCacheControl | [サイト画像](../../users-guide/site/site-image.md)のキャッシュに関する設定を行います。 |

### OutputCacheControl

OutputCacheControlで設定可能なパラメータは以下の通りです。

| パラメータ名         | 設定例 | 説明                                                                                                            |
| :------------------- | :----- | :-------------------------------------------------------------------------------------------------------------- |
| NoOutputCacheControl | false  | true<br>サイト画像のキャッシュを無効化します。<br><br>false（既定値）<br>サイト画像のキャッシュを有効化します。 |
| OutputCacheDuration  | 86400  | キャッシュの有効期限を秒単位で指定します。                                                                      |

## 対応バージョン

| 対応バージョン | 内容                   |
| :------------- | :--------------------- |
| 1.4.5.0以降    | OutputCache.jsonを追加 |

## 関連情報

-   [パラメータ変更時の確認事項](parameter-edit.md)
-   [サイト画像の設定と削除](../../users-guide/site/site-image.md)
