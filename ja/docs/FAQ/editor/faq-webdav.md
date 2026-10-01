---
title: 新規作成はできるが、更新・削除ができない（Windows）
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-webdav
translationKey: faq-webdav
shortname: ''
created: 2024-07-02
updated: 2024-07-02
---

## 回答

WebDAV発行が有効になっていることが原因です。

---

## 概要

Windows環境でプリザンターを構築後、テーブルへの新規登録は正常に処理できるが、更新ボタンや削除ボタンをクリックすると、ボタンアイコンが待機中のままで全く進展しない場合は、「WebDAV発行」が有効になっていることが原因です。

![更新ボタンのアイコンが待機中のまま止まっている状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/21b938fd9a9b450c93117de98f57c531.png)

## 解決方法

以下1または2のどちらかの手順で対応してください。

1.  「Windowsの機能の有効化と無効化（または役割と機能の追加）」より「WebDAV発行」のチェックをOFFにしてください。

    ![「Windowsの機能の有効化と無効化」で「WebDAV発行」のチェックを外すところ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/e825062cec8142c08b243bb88f377832.png)

1.  \web\pleasanter\Implem.Pleasanter\web.configに以下赤枠内を追記してください。

    ![web.config に追記する内容を赤枠で示した図](https://pleasanter.org/files/images/ja/FAQ/editor/assets/99b416e535d94865a673599dc18e4e7d.png)

    ```xml title="web.config" linenums="14" hl_lines="14-16 18"
        <modules>
          <remove name="WebDAVModule" />
        </modules>
        <handlers>
          <remove name="WevDAV" />
    ```

    web.config追記後にログイン画面でエラー表示する場合は、「Windowsの機能の有効化と無効化（または役割と機能の追加）」より以下4つをチェックしてください。

    -   .NET 拡張機能 4.8
    -   ASP.NET 4.8
    -   ISAPI フィルター
    -   ISAPI 拡張

    ![「Windowsの機能の有効化と無効化」で4つの機能にチェックを入れるところ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/687d475afc37445c9d7139a63b8156ae.png)
