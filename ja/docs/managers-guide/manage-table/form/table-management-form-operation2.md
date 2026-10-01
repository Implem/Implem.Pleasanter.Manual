---
title: より安全に利用するための設定
category: フォーム
order: '300'
status: ''
parts: ''
urlstring: table-management-form-operation2
translationKey: table-management-form-operation2
shortname: フォーム：操作手順2
created: 2025-11-18
updated: 2025-12-09
---

**[≪ テーブルの管理：フォーム：基本設定](table-management-form-operation1.md)**

## 5. CAPTCHAでボットによる不正アクセスを抑止する

フォーム機能は、Webサイトをボットによる不正アクセスから守るためのセキュリティサービスの1つである「CAPTCHA」をサポートしています。本機能がサポートしているCAPTCHAサービスは、以下の3つです。

1. [Cloudflare Turnstile](https://www.cloudflare.com/ja-jp/)
1. [Google reCAPTCHA v3](https://cloud.google.com/security/products/recaptcha)（ユーザ操作は不要）
1. [Google reCAPTCHA v2](https://cloud.google.com/security/products/recaptcha)（ユーザ操作が必要）

### 5.1. サイトキーとシークレットキーの入手

以下のリンク先から利用開始手続きを行い、サイトキー（Site Key）とシークレットキー（Secret Key）を入手してください。

1. [Cloudflare Turnstile](https://dash.cloudflare.com/sign-up)
1. [Google reCAPTCHA v3](https://www.google.com/recaptcha/admin/create?hl=ja)
1. [Google reCAPTCHA v2](https://www.google.com/recaptcha/admin/create?hl=ja)

なお、各サービスの詳細については、各サービス提供会社のWebサイトを確認してください。

### 5.2. CAPTCHAの設置

以下では、サービスごとの設定手順を説明します。なお、設定が済むと、ページの下部にバッジが表示されますが、バッジの表示位置は変更できません。

??? note "Cloudflare Turnstileの場合はこちら"

    設定ファイル[Security.json](../../../setup/parameters/security-json.md)のパラメータ"CaptchaConfig"を以下のように編集します。

    サイトキーとシークレットキーは、入手した各キーに置き換えてください

    ```json title="Security.json"
        "CaptchaConfig": {
            "Type": "Turnstile",
            "SiteKey": "サイトキー",
            "SecretKey": "シークレットキー"
        }
    ```

    Webブラウザで公開アドレスを開くと、ページ下部（コマンドボタンエリアの直前、左右中央）にバッジが表示され、自動的に検証が始まります。なお、場合によっては自動で検証されず、手動での対応が必要となります。これは、プリザンターで制御しているわけではありません。Turnstileの仕様です。

    ![Cloudflare Turnstileのバッジが公開ページ下部に表示され、検証中の状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/6a9e548d2963435e8462e8702c576160.png)

    検証完了後の表示は以下の通りです。

    ![Cloudflare Turnstileの検証が完了したあとの表示](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/d016c4ea0ddf4f37b5d6bc17b3a19f5f.png)

    プライバシーポリシー（Privacy）や利用許諾契約書（Terms）へのリンクが表示されているため、本番運用の際は必ず確認してください。

??? note "Google reCAPTCHA v3の場合はこちら"

    設定ファイル[Security.json](../../../setup/parameters/security-json.md)のパラメータ"CaptchaConfig"を以下のように編集します。

    サイトキーとシークレットキーは、入手した各キーに置き換えてください

    ```json title="Security.json"
        "CaptchaConfig": {
            "Type": "RecaptchaV3",
            "SiteKey": "サイトキー",
            "SecretKey": "シークレットキー",
            "RecaptchaV3": {
                "DefaultScoreThreshold": "0.7"
            }
        }
    ```

    Webブラウザで公開アドレスを開くと、自動的に検証が実行され、ページの右下隅にバッジが表示されます。バッジには、プライバシーポリシーや利用許諾契約書へのリンクが表示されます。また、Googleは、日本のユーザ向けに[個人情報の保護に関する法律、電気通信事業法に基づく事項を開示](https://policies.google.com/privacy/additional?hl=en)しています。本番運用の際は確認してください。

    ![Google reCAPTCHA v3のバッジがページの右下隅に表示された状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/759c479284fc44ed8384a132ed53509d.png)

    バッジにカーソルを合わせると、表示が展開します。

    ![Google reCAPTCHA v3のバッジにカーソルを合わせて展開した状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/f8f045974f2a42c9b393585d969e9257.png)

??? note "Google reCAPTCHA v2の場合はこちら"

    設定ファイル[Security.json](../../../setup/parameters/security-json.md)のパラメータ"CaptchaConfig"を以下のように編集します。

    サイトキーとシークレットキーは、入手した各キーに置き換えてください

    ```json title="Security.json"
        "CaptchaConfig": {
            "Type": "RecaptchaV2",
            "SiteKey": "サイトキー",
            "SecretKey": "シークレットキー"
        }
    ```

    Webブラウザで公開アドレスを開くと、ページ下部（コマンドボタンエリアの直前、左右中央）にバッジが表示されます。バッジには、プライバシーポリシーや利用許諾契約書へのリンクが表示されます。また、Googleは、日本のユーザ向けに[個人情報の保護に関する法律、電気通信事業法に基づく事項を開示](https://policies.google.com/privacy/additional?hl=en)しています。本番運用の際は確認してください。

    ![Google reCAPTCHA v2のバッジが公開ページ下部に表示された状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/135b38df1a574c0d8c1f3356f4c665e9.png)

    チェックボックスをクリックすると、検証が実行されます。検証が完了すると、次のように表示されます。

    ![Google reCAPTCHA v2の検証が完了したあとの表示](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/331c218b87cb4ee0a1086c0b12ee038a.png)

### 5.3. CSPの設定

CAPTCHAサービスを正しく利用するには、CSP（コンテントセキュリティポリシー）の設定が必要です。

設定ファイル[Security.json](../../../setup/parameters/security-json.md)のパラメータ"ContentSecurityPolicy"配下のディレクティブを以下のように書き替え、保存してください。保存後、プリザンターを再起動すると、変更が反映されます。

書き替えるべきディレクティブは、CAPTCHAサービスプロバイダー（Cloudflare / Google）により異なります。

??? note "Cloudflare Turnstileの場合はこちら"

    Cloudflareが推奨する設定が変更される可能性もあります。[公式情報](https://developers.cloudflare.com/turnstile/reference/content-security-policy/)も合わせて確認してください。

    ``` json title="Security.json"
        "ContentSecurityPolicy": {
            "Enabled": false,
            "ReportOnlyEnabled": true,
            "Values": [
                {
                    "default-src": "'self'",
                    "script-src": "'self' 'strict-dynamic' https://challenges.cloudflare.com",
                    "script-src-attr": "'self' 'unsafe-inline'",
                    "script-src-elem": "",
                    "style-src": "'self'",
                    "style-src-attr": "'self' 'unsafe-inline'",
                    "style-src-elem": "'self' 'unsafe-inline'",
                    "img-src": "'self' data:",
                    "font-src": "'self' data:",
                    "object-src": "'none'",
                    "connect-src": "'self'",
                    "frame-src": "'self' https://challenges.cloudflare.com",
                    "manifest-src": "",
                    "media-src": "",
                    "worker-src": "",
                    "base-uri": "'self'",
                    "form-action": "'self'",
                    "frame-ancestors": "",
                    "report-uri": "/CspReport/Report",
                    "report-to": "",
                    "sandbox": "",
                    "upgrade-insecure-requests": false
                }
            ]
    ```

??? note "Google reCAPTCHA（v3/v2共通）の場合はこちら"

    Googleが推奨する設定が変更される可能性もあります。[公式情報](https://developers.google.com/recaptcha/docs/faq?hl=ja#im-using-content-security-policy-csp-on-my-website.-how-can-i-configure-it-to-work-with-recaptcha)も合わせて確認してください。

    ``` json title="Security.json"
        "ContentSecurityPolicy": {
            "Enabled": false,
            "ReportOnlyEnabled": true,
            "Values": [
                {
                    "default-src": "'self'",
                    "script-src": "'self' 'strict-dynamic' https://www.google.com/recaptcha https://www.gstatic.com/recaptcha",
                    "script-src-attr": "'self' 'unsafe-inline'",
                    "script-src-elem": "",
                    "style-src": "'self'",
                    "style-src-attr": "'self' 'unsafe-inline'",
                    "style-src-elem": "'self' 'unsafe-inline'",
                    "img-src": "'self' data:",
                    "font-src": "'self' data:",
                    "object-src": "'none'",
                    "connect-src": "'self' https://www.google.com/recaptcha",
                    "frame-src": "'self' https://www.google.com https://www.google.com/recaptcha https://recaptcha.google.com/recaptcha",
                    "manifest-src": "",
                    "media-src": "",
                    "worker-src": "",
                    "base-uri": "'self'",
                    "form-action": "'self'",
                    "frame-ancestors": "",
                    "report-uri": "/CspReport/Report",
                    "report-to": "",
                    "sandbox": "",
                    "upgrade-insecure-requests": false
                }
            ]
    ```

## 6. 未認証ユーザアクセス時のページ遷移設定

プリザンターにログインしていない状態で、プリザンターが解釈可能なURLへアクセスした場合、プリザンターはログイン画面へ遷移するように設計されています。フォーム機能の利用にあたり、この遷移がセキュリティ上の懸念となる場合は、設定ファイル[Security.json](../../../setup/parameters/security-json.md)のパラメータ"ShowLoginPageOnAuthError"の値をfalseに設定してください。

``` json title="Security.json"
    "ShowLoginPageOnAuthError": false,
```

|設定値|意味|
|:--|:--|
|true|ログイン画面に遷移します。既定の設定です。|
|false|404エラーとなります。遷移先のページでは、「戻る」ボタン、ロゴのリンクは表示されません。|

## 7. CAPTCHA機能を無効化する

フォーム機能を社内イントラネット内で利用する場合など、CAPTCHA機能が不要な場合は、設定ファイル[Security.json](../../../setup/parameters/security-json.md)のパラメータ"CaptchaConfig"を以下のように編集してください。

```json title="Security.json"
    "CaptchaConfig": {
        "Type": "None"
    }
```

また、CSPの設定を元の設定に戻してください。

## 関連情報

-   [テーブルの管理：フォーム：基本設定](table-management-form-operation1.md)
-   [Cloudflare Turnstile](https://www.cloudflare.com/ja-jp/)
-   [Google reCAPTCHA v3](https://cloud.google.com/security/products/recaptcha)
-   [Cloudflare Turnstile](https://dash.cloudflare.com/sign-up)
-   [Google reCAPTCHA v3](https://www.google.com/recaptcha/admin/create?hl=ja)
-   [個人情報の保護に関する法律、電気通信事業法に基づく事項を開示](https://policies.google.com/privacy/additional?hl=en)
-   [公式情報](https://developers.cloudflare.com/turnstile/reference/content-security-policy/)
-   [公式情報](https://developers.google.com/recaptcha/docs/faq?hl=ja#im-using-content-security-policy-csp-on-my-website.-how-can-i-configure-it-to-work-with-recaptcha)
