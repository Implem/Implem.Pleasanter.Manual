---
title: バージョンアップ作業でCodeDefinerを実行したら「same key has already been added」というエラーが発生した
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-codedefiner-error-same-key
translationKey: faq-codedefiner-error-same-key
shortname: ''
created: 2024-07-18
updated: 2024-07-18
---

## 回答

App_Data\DisplaysフォルダのメッセージファイルのIDが重複しています。新バージョンのフォルダ一式を旧バージョンに上書きしないでください。

---

## 概要

バージョンアップ作業にてCodeDefiner実行時に以下のような「same key has already been added」が発生する場合は、App_Data\DisplaysフォルダにあるメッセージファイルのIDが重複していることが原因です。

``` text
<ERROR> Starter.Main: UnhandledException : An item with the same key has already been added. Key: SiteXX.json
   at System.Collections.Generic.Dictionary`2.TryInsert(TKey key, TValue value, InsertionBehavior behavior)
～以下略～
```

旧バージョンのフォルダへ上書きせず、別のフォルダ名にリネームするなどしてバックアップした後に新バージョン配置してください。

## 関連情報

-   [プリザンターのバージョンアップ手順(Azure App Service)](../../setup/version-up-migration/version-up-manually/version-up-azure.md)
-   [プリザンターのバージョンアップ手順(Linux)](../../setup/version-up-migration/version-up-manually/version-up-net-core.md)
-   [プリザンターのバージョンアップ手順(Windows)](../../setup/version-up-migration/version-up-manually/version-up-net.md)
