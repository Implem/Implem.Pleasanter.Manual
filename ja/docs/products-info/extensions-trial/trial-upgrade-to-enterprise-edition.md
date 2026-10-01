---
title: Enterprise Editionへのアップグレード
order: '1800'
translationKey: trial-upgrade-to-enterprise-edition
created: 2025-04-02
updated: 2025-12-03
---

## 概要

トライアル期間中またはトライアル期限切れの状態からEnterprise Editionへ拡張した項目を維持した状態でアップグレードすることができます。

## 操作手順

アップグレードは以下の手順で実施してください。

### :one: トライアル開始時に「/e」オプションを利用しなかった場合<br>（分類項目100個を追加した状態）

<div class="steps" markdown>

1.  「Community EditionからEnterprise Editionへのアップグレード手順」の操作手順2.を実行してください。
1.  「Community EditionからEnterprise Editionへのアップグレード手順」の操作手順3.を実行してください。Enterprise Editionにアップグレードします。
1.  「項目拡張手順（ver.1.4.8以降）」の操作手順「2. Issues.jsonおよびResults.jsonの編集、格納」を実施してください。  
    このとき、Issues.jsonとResults.jsonの"Class"に100を設定してください。以下にサンプルを提示します。

    ```json linenums="1" hl_lines="4" title="Issues.json：期限付きテーブル"
    {
            "TableName": "Issues",
            "ReferenceType": "Issues",
            "Class": 100,
            "Num": 0,
            "Date": 0,
            "Description": 0,
            "Check": 0,
            "Attachments": 0
    }
    ```

    ```json linenums="1" hl_lines="4" title="Results.json：記録テーブル"
    {
        "TableName": "Results",
        "ReferenceType": "Results",
        "Class": 100,
        "Num": 0,
        "Date": 0,
        "Description": 0,
        "Check": 0,
        "Attachments": 0
    }
    ```

1.  「項目拡張手順（ver.1.4.8以降）」の操作手順「3. CodeDefinerの実行」を実施してください。
1.  「項目拡張手順（ver.1.4.8以降）」の操作手順「4. 項目拡張の確認」を実施してください。
1.  トライアル時に拡張した項目（分類001～分類100）が表示することを確認してください。

</div>

### :two: トライアル開始時に「/e」オプションを利用した場合<br>（Issues.json、Results.jsonを設定した場合）

<div class="steps" markdown>

1.  「Community EditionからEnterprise Editionへのアップグレード手順」の操作手順2.を実施してください。
1.  「Community EditionからEnterprise Editionへのアップグレード手順」の操作手順3.を実施してください。Enterprise Editionにアップグレードします。
1.  「項目拡張手順（ver.1.4.8以降）」の操作手順「4. 項目拡張の確認」を実施してください。
1.  トライアル時に拡張した項目（数値001、日付002等）が表示することを確認してください。

</div>

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.4.15.0以降   | 機能追加 |

## 関連情報

-   [Pleasanter Extensionsのトライアル](../../developers-guide/index.md)
-   [トライアルの案内ページ](../../developers-guide/index.md)
-   [Enterprise Editionの案内ページ](https://pleasanter.org/extensions-trial-ended-info/?utm_source=installer&utm_medium=app&utm_campaign=extension-trial&utm_content=route03)
-   [手動バージョンアップ](../../setup/version-up-migration/version-up-manually/index.md)
-   [CodeDefinerのコマンド一覧](../../setup/codedefiner/codedefiner-command.md)
