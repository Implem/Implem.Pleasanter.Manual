---
title: CodeDefinerを使ったトライアル期間中のバージョンアップ
order: '1600'
translationKey: trial-period-updates-codedefiner
created: 2025-04-02
updated: 2025-12-03
---

## 概要

トライアル期間中にプリザンターをバージョンアップする方法を説明します。トライアル期間中のプリザンターのバージョンアップには、以下の2つの方法があります。

1. インストーラを使う方法
1. CodeDefinerを使う方法

このページでは、CodeDefinerを使う方法を説明します。

!!! tip "インストーラを使う方法"
    インストーラを使う方法は、こちらを参照してください。

### CodeDefinerを使う方法

[手動バージョンアップの手順](../../setup/version-up-migration/version-up-manually/index.md)でバージョンアップを行い、手順内のCodeDefiner実行時は、以下の通り`trial`コマンドで実行してください。

``` text title="Windowsの実行例"
cd C:\web\pleasanter\Implem.CodeDefiner
dotnet Implem.CodeDefiner.dll trial
```

!!! danger
    通常のバージョンアップ手順（`_rds`コマンド）で実行するとトライアルで増やした項目が削除されるため、データが消失する場合があります。

!!! tip "CodeDefinerのコマンド"
    CodeDefinerのコマンドについては、[こちら](../../setup/codedefiner/codedefiner-command.md)を確認してください。

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
