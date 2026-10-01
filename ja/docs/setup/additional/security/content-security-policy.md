---
title: コンテンツセキュリティポリシー機能
category: 追加設定：セキュリティ
order: '100'
status: ''
parts: ''
urlstring: content-security-policy
translationKey: content-security-policy
shortname: コンテンツセキュリティポリシー機能
created: 2025-07-29
updated: 2025-08-12
---

## 概要

プリザンターにコンテンツセキュリティポリシーを設定するための機能です。

## 前提条件

事前に[Security.json](../../parameters/security-json.md) の ContentSecurityPolicy パラメータの設定を編集する必要があります。詳細につきましては [Security.json](../../parameters/security-json.md) を参照してください。パラメータ変更後は[パラメータ変更時の確認事項](../../parameters/parameter-edit.md)を確認してください。

## コンテンツセキュリティポリシー

コンテンツセキュリティポリシー（以下CSP）はWebブラウザがどのリソース（スクリプト、画像、スタイルなど）をどこから読み込むかを制御するWebセキュリティ機能です。
CSPの詳細については、[MDN Web Docs: Content Security Policy (CSP) ガイド](https://developer.mozilla.org/ja/docs/Web/HTTP/Guides/CSP) を参照してください。

## CSP設定

CSP違反の検出のみ行いたい場合は ReportOnlyEnabled > true を設定してください。CSP違反を検出した場合はブラウザのコンソールログとレポートファイルにCSP違反の内容を出力します。
CSP違反の検出と該当リソースの読み込み停止を行いたい場合は Enabled > true を設定してください。CSP違反を検出した場合は該当リソースの読み込みを停止しブラウザのコンソールログとレポートファイルにCSP違反の内容を出力します。

## CSP違反例

[Security.json](../../parameters/security-json.md)で ContentSecurityPolicy > Values > img-src > 'self' を設定した場合のCSP違反例となります。

### Enabled > true の場合

<details markdown="1">
<summary>ブラウザのコンソールログ</summary>

![Enabledがtrueのときのブラウザのコンソールログ。CSP違反が出力されている](https://pleasanter.org/files/images/ja/setup/additional/security/assets/380624830c0648038bb7b4d98c24ff79.png)

</details>

<details markdown="1">
<summary>CSP違反レポートファイル</summary>

```
2025-07-30 17:34:51.2576 | IP: ::1 | ContentType: application/csp-report | UserAgent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Safari/537.36 | body: {"csp-report":{"document-uri":"http://localhost:59802/users/login?ReturnUrl=%2F","referrer":"","violated-directive":"img-src","effective-directive":"img-src","original-policy":"default-src 'self'; script-src 'self' 'strict-dynamic' 'nonce-ddr+pcp5Pwo3r/5JusK6JA=='; script-src-attr 'self' 'unsafe-inline'; style-src 'self' 'nonce-ddr+pcp5Pwo3r/5JusK6JA=='; style-src-attr 'self' 'unsafe-inline'; style-src-elem 'self' 'unsafe-inline'; img-src 'self'; font-src 'self' data:; object-src 'none'; connect-src 'self' http://localhost:* ws://localhost:* wss://localhost:*; frame-src 'none'; base-uri 'self'; form-action 'self'; report-uri /CspReport/Report;","disposition":"enforce","blocked-uri":"data","line-number":2,"column-number":51704,"source-file":"http://localhost:59802/assets/plugins/jquery-3.6.0.min.js","status-code":200,"script-sample":""}}
2025-07-30 17:34:51.2576 | IP: ::1 | ContentType: application/csp-report | UserAgent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Safari/537.36 | body: {"csp-report":{"document-uri":"http://localhost:59802/users/login?ReturnUrl=%2F","referrer":"","violated-directive":"img-src","effective-directive":"img-src","original-policy":"default-src 'self'; script-src 'self' 'strict-dynamic' 'nonce-ddr+pcp5Pwo3r/5JusK6JA=='; script-src-attr 'self' 'unsafe-inline'; style-src 'self' 'nonce-ddr+pcp5Pwo3r/5JusK6JA=='; style-src-attr 'self' 'unsafe-inline'; style-src-elem 'self' 'unsafe-inline'; img-src 'self'; font-src 'self' data:; object-src 'none'; connect-src 'self' http://localhost:* ws://localhost:* wss://localhost:*; frame-src 'none'; base-uri 'self'; form-action 'self'; report-uri /CspReport/Report;","disposition":"enforce","blocked-uri":"data","status-code":200,"script-sample":""}}
```

</details>

### ReportOnlyEnabled > true の場合

<details markdown="1">
<summary>ブラウザのコンソールログ</summary>

![ReportOnlyEnabledがtrueのときのブラウザのコンソールログ](https://pleasanter.org/files/images/ja/setup/additional/security/assets/3f8361a19b8b43c6979737441ea49fbb.png)

</details>

<details markdown="1">
<summary>CSP違反レポートファイル</summary>

```
2025-07-30 17:26:45.0399 | IP: ::1 | ContentType: application/csp-report | UserAgent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Safari/537.36 | body: {"csp-report":{"document-uri":"http://localhost:59802/users/login","referrer":"http://localhost:59802/","violated-directive":"img-src","effective-directive":"img-src","original-policy":"default-src 'self'; script-src 'self' 'strict-dynamic' 'nonce-0dFRrHOEwmad01cIBlHpOQ=='; script-src-attr 'self' 'unsafe-inline'; style-src 'self' 'nonce-0dFRrHOEwmad01cIBlHpOQ=='; style-src-attr 'self' 'unsafe-inline'; style-src-elem 'self' 'unsafe-inline'; img-src 'self'; font-src 'self' data:; object-src 'none'; connect-src 'self' http://localhost:* ws://localhost:* wss://localhost:*; frame-src 'none'; base-uri 'self'; form-action 'self'; report-uri /CspReport/Report;","disposition":"report","blocked-uri":"data","line-number":2,"column-number":51704,"source-file":"http://localhost:59802/assets/plugins/jquery-3.6.0.min.js","status-code":200,"script-sample":""}}
2025-07-30 17:26:45.0462 | IP: ::1 | ContentType: application/csp-report | UserAgent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Safari/537.36 | body: {"csp-report":{"document-uri":"http://localhost:59802/users/login","referrer":"http://localhost:59802/","violated-directive":"img-src","effective-directive":"img-src","original-policy":"default-src 'self'; script-src 'self' 'strict-dynamic' 'nonce-0dFRrHOEwmad01cIBlHpOQ=='; script-src-attr 'self' 'unsafe-inline'; style-src 'self' 'nonce-0dFRrHOEwmad01cIBlHpOQ=='; style-src-attr 'self' 'unsafe-inline'; style-src-elem 'self' 'unsafe-inline'; img-src 'self'; font-src 'self' data:; object-src 'none'; connect-src 'self' http://localhost:* ws://localhost:* wss://localhost:*; frame-src 'none'; base-uri 'self'; form-action 'self'; report-uri /CspReport/Report;","disposition":"report","blocked-uri":"data","status-code":200,"script-sample":""}}
```

</details>

## CSP違反レポートファイルの格納場所

※標準構成の場合、CSP違反レポートファイルは下記のディレクトリに格納されています。

|環境|格納場所|
|:--|:--|
|Windows|C:\web\pleasanter\Implem.Pleasanter\Logs|
|Linux|/web/pleasanter/Implem.Pleasanter/Logs|
|Microsoft Azure|.\Implem.Pleasanter\Logs|

## 開発時のCSP違反

Visual Studioからプリザンターを起動した場合に下記のCSP違反がブラウザのコンソールログに出力されますがCSP違反レポートファイルに出力しません。

- `Refused to load the script 'http://localhost:XXXXX/_vs/browserLink' because ・・・`
- `Refused to load the script 'http://localhost:XXXXX/_framework/aspnetcore-browser-refresh.js' because ・・・`

<details markdown="1">
<summary>ブラウザのコンソールログ（ReportOnlyEnabled > true）</summary>

![Visual Studioからの起動時に出るCSP違反のブラウザのコンソールログ](https://pleasanter.org/files/images/ja/setup/additional/security/assets/fcc961319989403582f881bd4bc90650.png)

</details>
上記CSP違反はVisual Studioがデバッグ用に自動的にHTMLソースコードへ追加する影響によるものです。
Visual Studioでの開発時以外はHTMLソースコードへ追加されません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.19.0 以降|機能追加|

## 関連情報

-   [パラメータ設定：Security.json](../../parameters/security-json.md)
-   [Security.json](../../parameters/security-json.md)
-   [パラメータ設定：パラメータ変更時の確認事項](../../parameters/parameter-edit.md)
-   [MDN Web Docs: Content Security Policy (CSP) ガイド](https://developer.mozilla.org/ja/docs/Web/HTTP/Guides/CSP)
