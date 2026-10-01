---
title: Enterprise Editionアップグレード済みプリザンターのバージョンアップ手順(インストーラ利用)
category: バージョンアップ手順
order: '300'
status: ''
parts: ''
urlstring: enterprise-edition-version-up-installer
translationKey: enterprise-edition-version-up-installer
shortname: Enterprise Edition,アップグレード済みプリザンターのバージョンアップ
created: 2025-01-24
updated: 2025-03-27
---

## 概要

Enterprise Editionご利用中の環境においてプリザンターをバージョンアップする際の手順について説明します。特に項目拡張を行っている場合は必ず本手順を確認してください。

## 注意事項

1.  バージョンアップ作業前にデータベースバックアップを必ず取得してください。  
    [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)
1.  ライセンスファイルは必ず現在契約中のものを使用してください。特に項目拡張を行っている場合、期限切れのライセンスファイルを用いてCodeDefinerを実行すると拡張した項目が削除され、入力済みデータを参照できなくなります。

## 前提条件

1.  本手順はプリザンターをEnterprise Editionにアップグレードしていることを前提とします。

## 操作手順

本手順は弊社オンラインマニュアルの「バージョンアップ(インストーラ)」を参照して進めてください。  
[Pleasanter ユーザーマニュアル - バージョンアップ(インストーラ)](../../../setup/version-up-migration/version-up-installer/index.md)

### 1. バージョンアップ手順の「インストーラの実行」まで実施

弊社オンラインマニュアルにそってバージョンアップ作業の手順4「インストーラの実行」まで実施します。

=== ":fontawesome-brands-windows: Windows環境"

    「インストーラを利用したバージョンアップ手順(Windows)」

=== ":fontawesome-brands-linux: Linux環境"

    「インストーラを利用したバージョンアップ手順(Linux)」

=== ":material-microsoft-azure: Azure App Service環境"

    「インストーラを利用したバージョンアップ手順(Azure App Service)」

手順4「インストーラの実行」にて項目拡張の使用数削減が起こる場合、エラーメッセージ「`<ERROR> Configurator.CheckColumnsShrinkage: The columns will be shrinked.`」が表示されて終了し、CodeDefinerは実行されません。エラーとなった場合は下図のように削減する項目が表示されますので、パラメータファイルおよびライセンスが正しく適用されているか再度確認ください。

![項目の削減が発生してCodeDefinerがエラー終了したログ](https://pleasanter.org/files/images/ja/products-info/enterprise-edition/version-up/assets/b631d5eda9d34df484581981a2349834.png)

項目の削減を許容する場合は、手順4「インストーラの実行」で実行するコマンドに引数「--force」を指定して、実行してください。

``` bat
pleasanter-setup --force
```

### 2. バージョンアップの確認

<div class="steps" markdown>

1.  プリザンターにログインし、ナビゲーションメニューの「ヘルプ」－「バージョン」より以下を確認してください。
    - ライセンスが「商用ライセンス」となっていること
    - ライセンス期限が正しいこと（2月末までのライセンスの場合、3/1と表示されます）
    - 使用者が正しいこと
    - バージョンが正しいこと
1.  項目拡張済みの場合は以下を確認してください。
    - 任意のテーブルを開き、ナビゲーションメニューの[管理]-[テーブルの管理]より[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブにて、選択肢一覧のリストに拡張した項目（分類001、数値001等）が表示されること
    - 拡張した項目を設定したテーブルの編集画面を開き、項目がすべて表示していること

</div>

## 関連情報

-   [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)
-   [Pleasanter ユーザーマニュアル - バージョンアップ(インストーラ)](../../../setup/version-up-migration/version-up-installer/index.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
