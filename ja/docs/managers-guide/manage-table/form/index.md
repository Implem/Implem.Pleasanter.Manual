---
title: フォーム
category: フォーム
order: '100'
status: ''
parts: ''
urlstring: table-management-form
translationKey: table-management-form
shortname: フォーム
created: 2025-11-18
updated: 2026-06-29
---

## 概要

任意のテーブル（記録テーブルまたは期限付きテーブル）を、プリザンターのアカウントを持たない外部ユーザに対して、期間を限定して公開する「フォーム機能」について説明します。外部ユーザは、公開アドレスにアクセスすることで、レコードを作成できるようになります。

以下は、フォーム機能を使って公開したレコード作成画面の見本です。

### フォーム機能を使って公開したレコード作成画面の見本

![外部ユーザ向けに公開されたレコード作成画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/dfec0a0f04d445ffb97e4c4e2e4b5c28.png)

### サンクスメッセージ

アンケートなどに使用したケースにおいて、回答者に対して伝達事項を表示する機能を備えます。

![レコード作成後に回答者へ表示されるサンクスメッセージの画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/f6cc4a514cb04915be58fe9d491206ad.png)

### 利用不可メッセージ

公開期間外に公開ページへアクセスした場合に、利用できない旨を表示する機能を備えます。

![公開期間外にアクセスしたときに表示される利用不可メッセージの画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/6775f73332b2495d857eed12b48b59f4.png)

## 注意事項

1. フォーム機能をアンケートなど、不特定多数からの情報収集に活用する場合は、個人情報の保護に関する法律などの関連法を遵守してください。
1. フォーム機能を使い、組織外部の不特定多数に向けて公開する場合は、SSL/TLS（以下、TLSと表記）の導入を推奨します。TLSの導入にあたっては、TLSサーバ証明書の取得が必要です。プリザンターでは設定ファイル[Service.json](../../../setup/parameters/service-json.md)のパラメータ"RequireHttps"をtrueにすることで、httpsによる接続を強制することができます。
1. プリザンターにログインしていない状態で、プリザンターが解釈可能なURLへアクセスした場合、プリザンターはログイン画面へ遷移するように設計されています。フォーム機能の利用にあたり、この遷移がセキュリティ上の懸念となる場合は、設定ファイル[Security.json](../../../setup/parameters/security-json.md)のパラメータ"ShowLoginPageOnAuthError"の値をfalseに設定してください。
1. CAPTCHA機能利用時は有償となる場合があります。詳細は各サービスサイトをご確認ください。  
   1. [Cloudflare Turnstile](https://www.cloudflare.com/ja-jp/)
   1. [Google reCAPTCHA v3/v2](https://cloud.google.com/security/products/recaptcha)
1. 公開の開始日時と終了日時はUTC（JSTの9時間前）で設定する必要があります。

## 制限事項

1. フォーム機能の有効化・無効化には、プリザンターの再起動が必要です。
1. フォーム機能がサポートするCAPTCHA機能の有効化・無効化時には、プリザンターの再起動が必要です。
1. フォーム機能を有効化した場合、設定ファイル[Security.json](../../../setup/parameters/security-json.md)のパラメータ"TokenCheck"は機能しません（ASP.NET Core標準のCSRF対策を組み込んでいるため、CSRF対策は常に動作します）。
1. 選択肢一覧のリンク（例えば、選択肢一覧での[[8882]]のような設定）は、リンクは「[情報公開機能](../publish/table-management-publish.md)」を有効化したテーブルに限り使用可能です。
1. ログインしているユーザの権限で動作しない一部のスクリプト、サーバスクリプトは動作しません。詳細は[スクリプト](../../../developers-guide/script/index.md)の「スクリプトの権限に関する注意事項」および[サーバスクリプト](../../../developers-guide/server-script/index.md)の「サーバスクリプトの権限に関する注意事項」を参照してください。
1. 公開画面（レコード作成画面、サンクスメッセージ、利用不可メッセージ）の左上に表示されるテナントロゴは変更することができません（テナントの管理画面における設定は反映されません）。
1. サイト画像とサイトのタイトルを公開画面に表示させるには、タイトル項目を有効化する必要があります。サイトのタイトルを表示させつつ、タイトル項目を公開画面に表示させないためには、タイトル項目の詳細設定画面で「[非表示](../editor/editor-settings/advanced-settings/general/table-management-hide.md)」を有効化してください。

## 前提条件

1. フォーム機能の有効化・無効化には、サイトの管理権限が必要です。
1. CAPTCHA機能の有効化・無効化には、サイトの管理権限が必要です。
1. CAPTCHA機能の利用には、対応サービスから「サイトキー」と「シークレットキー」を取得しておく必要があります。

## 操作手順

以下の流れで説明します。

1. [フォーム機能を有効化する](table-management-form-operation1.md)
1. [公開用のテーブルを作成する](table-management-form-operation1.md)
1. [テーブルの公開機能を有効化する](table-management-form-operation1.md)
1. [カスタムメッセージの作成](table-management-form-operation1.md)
1. [CAPTCHAでボットによる不正アクセスを抑止する](table-management-form-operation2.md)
1. [未認証ユーザアクセス時のページ遷移設定](table-management-form-operation2.md)

## 対応バージョン

| 対応バージョン     | 内容     |
| :----------------- | :------- |
| バージョン1.4.23.0 | 機能追加 |

## 関連情報

-   [Cloudflare Turnstile](https://www.cloudflare.com/ja-jp/)
-   [Google reCAPTCHA v3/v2](https://cloud.google.com/security/products/recaptcha)
-   [テーブルの管理：フォーム：基本設定](table-management-form-operation1.md)
-   [テーブルの管理：フォーム：より安全に利用するための設定](table-management-form-operation2.md)