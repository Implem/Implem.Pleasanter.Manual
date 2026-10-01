---
title: トップ画面を特定のページにしたい。
category: FAQ：トップ・サイトメニュー
order: '0'
status: ''
parts: ''
urlstring: faq-top-url-and-login-after-url
translationKey: faq-top-url-and-login-after-url
shortname: ''
created: 2020-08-01
updated: 2024-04-29
---

## 回答

[Locations.json](../../setup/parameters/locations-json.md)の「TopUrl」でトップ画面に設定したいページを設定してください。

---

## 概要

[Locations.json](../../setup/parameters/locations-json.md)の「TopUrl」でトップ画面に設定したいページのURLを設定できます。

## 設定手順

以下は`"http(s)://{サーバ名}/items/123/index"`をトップ画面のURLに設定する方法です。

1.  [Locations.json](../../setup/parameters/locations-json.md)を開いてください。
1.  パラメータTopUrlへ上記のURLを設定してください。サーバ名以降の文字列は適切に（例：`/items/123`）編集してください。

    ``` json title="Locations.json" linenums="1" hl_lines="2"
    {
        "TopUrl": "/items/123/index",
        "LoginAfterUrl": null // (1)!
    }
    ```

    1.  LoginAfterUrlはログイン後に遷移するページを設定するパラメータです。

1.  Webサーバまたはプリザンターを再起動してください。
1.  プリザンターのログイン画面でログインIDとパスワードを入力し、「ログイン」ボタンをクリックしてください。
1.  ログイン後、画面左上のロゴまたは[パンくずリスト](../../users-guide/site/site-breadcrumb-list.md)の「トップ」リンクをクリックしてください。
1.  TopUrlで設定したURLへ遷移することを確認してください。

## 関連情報

-   [Locations.json](../../setup/parameters/locations-json.md)
