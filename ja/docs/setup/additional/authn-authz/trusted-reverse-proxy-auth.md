---
title: 信頼済みリバースプロキシ認証
category: 追加設定：認証
order: '700'
status: ''
parts: ''
urlstring: trusted-reverse-proxy-auth
translationKey: trusted-reverse-proxy-auth
shortname: 信頼済みリバースプロキシ認証
created: 2026-03-12
updated: 2026-08-12
---

## 概要

信頼済みリバースプロキシが付与するHTTPヘッダーからユーザ名を取得し、自動ログインする機能について説明します。

## 注意事項

1. 本機能は、クライアントが当該ヘッダーを直接偽装できない構成（リバースプロキシが必ずヘッダーを上書きする構成）でのみ使用してください。
1. 公開環境で適切なネットワーク制限なしに有効化すると、なりすましリスクがあります。

## パラメータTrustedProxyParametersの設定

以下を参考に、設定ファイル[Authentication.json](../../parameters/authentication-json.md)のパラメータTrustedProxyParametersを設定してください。

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Enabled|true|trueを指定すると機能を有効化します。<br>環境変数TRUSTED_PROXY_AUTH_ENABLEDが設定されている場合、その値が優先されます。|
|Header|"X-Forwarded-User"|ユーザ名が格納されているHTTPヘッダー名を指定します。<br>環境変数TRUSTED_PROXY_AUTH_HEADERが設定されている場合、その値が優先されます。|

##### Authentication.jsonの 設定例

```json
{
        : 省略
    "TrustedProxyParameters": {
        "Enabled": true,
        "Header": "X-Forwarded-User"
    }
}
```

## 環境変数による設定と優先順位

以下の環境変数が設定されている場合は、[Authentication.json](../../parameters/authentication-json.md)の値より優先されます。

|環境変数名|対応<br>パラメータ|動作|
|:--|:--|:--|
|TRUSTED_PROXY_AUTH_ENABLED|Enabled|**空文字以外の値**<br>機能が有効になります。true以外の値（例えば1など）でも有効化されます。|
|TRUSTED_PROXY_AUTH_HEADER|Header|**空でない場合**<br>この環境変数の値を使用します。<br><br>**空の場合**<br>[Authentication.json](../../parameters/authentication-json.md)のパラメータHeaderの値を使用します。|

## 送信元IPによる制限について

<span class="pl-attention">**特定の送信元からのリクエストのみを自動ログインの対象とするには、必ず[Security.json](../../parameters/security-json.md)のパラメータForwardedHeaders.KnownNetworksまたはForwardedHeaders.KnownProxiesを設定してください。詳細は[Security.json](../../parameters/security-json.md)を参照してください。**</span>

## 対応バージョン

|対応バージョン|内容|
|---|---|
|バージョン 1.5.3.0 以降|機能追加|

## 関連情報

-   [パラメータ設定：Authentication.json](../../parameters/authentication-json.md)
-   [パラメータ設定：Security.json](../../parameters/security-json.md)