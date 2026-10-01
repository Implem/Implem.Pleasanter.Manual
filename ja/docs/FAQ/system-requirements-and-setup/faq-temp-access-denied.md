---
title: '''...\pleasanter\App_Data\Temp\1E70...3C6.xlsm''へのアクセスが拒否されました、というエラーが表示される'
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-temp-access-denied
translationKey: faq-temp-access-denied
shortname: ''
created: 2020-03-17
updated: 2025-01-30
---

## 回答

プリザンターインストールフォルダの「App_Data\Temp」フォルダに権限を付与してください。

---

## 概要

インストール時に、下記のようなエラーが発生する場合、本ページ記載の手順で解決できる場合があります。

``` text
'C:inetpubwwwrootpleasanterApp_DataTemp1E70....22ED93C6.xlsm' is denied.
'C:inetpubwwwrootpleasanterApp_DataTemp1E70....22ED93C6.xlsm'へのアクセスが拒否されました。
```

1.  スタートメニューから「インターネット インフォメーション サービス (IIS) マネージャ」を起動します。
1.  「サイト」－「Default Web Site」－「pleasanter」－「App_Data」－「Temp」をクリックし、ウィンドウ右ペインの「アクセス許可の編集」をクリックします。

    ![IISマネージャーで Temp フォルダの「アクセス許可の編集」を開くところ](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/ad65d2b0fb0a4b37888f4066444b1624.png)

1.  Pleasanterのプロパティダイアログのセキュリティタブを開き、IIS_IUSERSを選択して編集ボタンをクリックし「変更」にチェックし権限を付与します[^1]。

    ![セキュリティタブ。IIS_IUSERS に「変更」の権限を与えるところ](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/e9713a0976b14f958571c1e340b9408b.png)

1.  変更を適用し、再度プリザンターにアクセスしてください。

[^1]: 「変更」にチェックを入れると「書き込み」にもチェックが付きます。
