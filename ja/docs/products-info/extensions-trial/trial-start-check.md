---
title: トライアル開始の確認
category: トライアル
order: '1300'
status: ''
parts: ''
urlstring: pleasanter-extensions-trial-start
translationKey: pleasanter-extensions-trial-start
shortname: トライアル開始の確認
created: 2025-12-01
updated: 2025-12-03
---

## 概要

[Pleasanter Extensionsトライアル](../../developers-guide/index.md)で、正しくトライアルを開始できているかどうかを確かめる方法を説明します。

## 操作手順

<div class="steps" markdown>

1.  プリザンターを再起動してください。

    === ":fontawesome-brands-windows: Windowsの場合"

        1.  インターネット インフォメーション サービス（IIS）マネージャーを開いてください。
        1.  左ペインより「サイト」－「Default Web Site」を選択し、右ペインの「再起動」をクリックしてください。

    === ":fontawesome-brands-linux: Linuxの場合"

        1.  以下のコマンドを実行してください。

            ``` bash
            sudo systemctl restart pleasanter
            ```

    === ":material-microsoft-azure: Azure App Serviceの場合"

        1.  App Serviceを開き、「再起動」をクリックしてください。

1.  プリザンターにアクセスし、ログイン画面に下図のようにトライアル実施中の情報が表示されていることを確認してください。

    ![ログイン画面に表示されるトライアル中の情報表示](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/e6fb67510c654d4bb2196f0ddf2ff94c.png)

1.  プリザンターにログインし、ナビゲーションメニューの「ヘルプ」－「バージョン」よりバージョン情報を開き、下図のようにトライアル実施中の情報が表示されていることを確認してください。

    ![バージョン情報画面に表示されるトライアル中の情報表示](https://pleasanter.org/files/images/ja/products-info/extensions-trial/assets/50df0f2bc5704134b1b3ed461875a4a4.png)

1.  プリザンターにログインし、任意のテーブルを開いてください。

1.  ナビゲーションメニューの「管理」－[テーブルの管理](../../managers-guide/manage-table/index.md)より[エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)タブにて、[選択肢一覧](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)に項目（分類001～分類100）が表示されることを確認してください。

</div>
