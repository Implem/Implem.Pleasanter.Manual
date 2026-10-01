---
title: Enterprise Editionアップグレード済みプリザンターのバージョンアップ手順
category: バージョンアップ手順
order: '500'
status: ''
parts: ''
urlstring: enterprise-edition-version-up
translationKey: enterprise-edition-version-up
shortname: Enterprise Edition,アップグレード済みプリザンターのバージョンアップ
created: 2025-01-24
updated: 2025-02-14
---

## 概要

Enterprise Editionご利用中の環境においてプリザンターをバージョンアップする際の手順について説明します。特に項目拡張を行っている場合は必ず本手順を確認してください。

環境やバージョンに応じて、以下の各ページを参照してください。

-   [Enterprise Editionアップグレード済みプリザンターのバージョンアップ手順(インストーラ利用)](enterprise-edition-version-up-installer.md)
-   [Enterprise Editionアップグレード済みプリザンターのバージョンアップ手順(ver.1.4.8以降)](enterprise-edition-version-up-1.4.8.md)
-   [Enterprise Editionアップグレード済みプリザンターのバージョンアップ手順(Docker利用)](enterprise-edition-version-up-docker.md)

## 注意事項

1.  バージョンアップ作業前にデータベースバックアップを必ず取得してください。  
    [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)
1.  ライセンスファイルは必ず現在契約中のものを使用してください。特に項目拡張を行っている場合、期限切れのライセンスファイルを用いてCodeDefinerを実行すると拡張した項目が削除され、入力済みデータを参照できなくなります。

## 前提条件

1.  本手順はプリザンターをEnterprise Editionにアップグレードしていることを前提とします。

## 操作手順

本手順は弊社オンラインマニュアルの「バージョンアップ(インストーラ)」を参照して進めてください。  
[Pleasanter ユーザーマニュアル - バージョンアップ(インストーラ)](../../../setup/version-up-migration/version-up-installer/index.md)

### 1. ライセンスファイルのバックアップ

ご利用中の環境からライセンスファイルをバックアップします。ファイルの格納先は下記の通りです。

=== ":fontawesome-brands-windows: Windows環境"

    C:\web\pleasanter\Implem.Pleasanter

=== ":fontawesome-brands-linux: Linux環境"

    /web/pleasanter/Implem.Pleasanter

=== ":material-microsoft-azure: Azure App Service環境"

    C:\home\site\wwwroot\

上記パスは弊社オンラインマニュアルの手順に従ってインストールした場合のものになります。ご利用中の環境に応じて適宜読み替えてください。

### 2. Issues.jsonおよびResults.jsonのバックアップ

ご利用中の環境が項目拡張済みの場合は、Issues.jsonおよびResults.jsonをバックアップします。ファイルの格納先は下記の通りです。項目拡張を行っていない場合は本処理は不要ですので3.に進んでください。

=== ":fontawesome-brands-windows: Windows環境"

    C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters\ExtendedColumns

=== ":fontawesome-brands-linux: Linux環境"

    /web/pleasanter/Implem.Pleasanter/App_Data/Parameters/ExtendedColumns

=== ":material-microsoft-azure: Azure App Service環境"

    C:\home\site\wwwroot\App_Data\Parameters\ExtendedColumns

上記パスは弊社オンラインマニュアルの手順に従ってインストールした場合のものになります。ご利用中の環境に応じて適宜読み替えてください。

### 3. バージョンアップ作業「4. プリザンターの配置」まで実施

弊社オンラインマニュアルにそってバージョンアップ作業の手順4「プリザンターの配置」まで実施します。

=== ":fontawesome-brands-windows: Windows環境"

    「プリザンターのバージョンアップ手順(Windows)」

=== ":fontawesome-brands-linux: Linux環境"

    「プリザンターのバージョンアップ手順(Linux)」

=== ":material-microsoft-azure: Azure App Service環境"

    「プリザンターのバージョンアップ手順(Azure App Service)」

### 4. ライセンスファイルの格納

1.でバックアップしたライセンスファイルをご利用中の環境に応じて以下フォルダにそれぞれ上書きコピーしてください。

=== ":fontawesome-brands-windows: Windows環境"

    C:\web\pleasanter\Implem.Pleasanter
    C:\web\pleasanter\Implem.CodeDefiner

=== ":fontawesome-brands-linux: Linux環境"

    /web/pleasanter/Implem.Pleasanter
    /web/pleasanter/Implem.CodeDefiner

=== ":material-microsoft-azure: Azure App Service環境"

    C:\web\pleasanter\Implem.Pleasanter
    C:\web\pleasanter\Implem.CodeDefiner  
    ※Azure App Serviceのバージョンアップ作業の手順4.3「パラメータ再設定」はローカル環境での作業となります。上記パスはローカル環境での作業パスを示します。

上記パスは弊社オンラインマニュアルの手順に従ってインストールした場合のものになります。ご利用中の環境に応じて適宜読み替えてください。  
格納するライセンスファイルは、ライセンスパックに含まれる「Implem.License.dll」を使用しても構いません。その場合は契約中のライセンスファイルであることを確認してください。

### 5. Issues.jsonおよびResults.jsonの格納

1.でバックアップしたIssues.jsonおよびResults.jsonをご利用中の環境に応じて以下フォルダにそれぞれ上書きコピーしてください。

=== ":fontawesome-brands-windows: Windows環境"

    C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters\ExtendedColumns

=== ":fontawesome-brands-linux: Linux環境"

    /web/pleasanter/Implem.Pleasanter/App_Data/Parameters/ExtendedColumns

=== ":material-microsoft-azure: Azure App Service環境"

    C:\home\site\wwwroot\App_Data\Parameters\ExtendedColumns

上記パスは弊社オンラインマニュアルの手順に従ってインストールした場合のものになります。ご利用中の環境に応じて適宜読み替えてください。

### 6. バージョンアップ作業の「5. CodeDefinerの実行」以降を実行

弊社オンラインマニュアルにそってバージョンアップ作業の手順5「CodeDefinerの実行」以降を実施します。

=== ":fontawesome-brands-windows: Windows環境"

    「プリザンターのバージョンアップ手順(Windows)」

=== ":fontawesome-brands-linux: Linux環境"

    「プリザンターのバージョンアップ手順(Linux)」

=== ":material-microsoft-azure: Azure App Service環境"

    「プリザンターのバージョンアップ手順(Azure App Service)」

### 7. バージョンアップの確認

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
