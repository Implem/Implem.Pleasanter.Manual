---
title: 1.4.8.0以降のバージョンアップ手順(Azure App Service)
category: バージョンアップ
order: '200'
status: ''
parts: ''
urlstring: version-up-azure-1.4.8.0
translationKey: version-up-azure-1.4.8.0
shortname: バージョンアップ手順,App Serviceのバージョンアップ手順
created: 2024-09-02
updated: 2026-01-13
---

## 概要

Azure App Serviceで運用しているプリザンターver1.4.8.0以降のバージョンアップ手順です。

## 注意事項

1.  現在運用中のパラメータファイルを最新バージョンに上書きコピーしないでください。最新バージョンで新たに追加したパラメータが失われ、プリザンターが起動しない恐れがあります。
1.  Enterprise Editionにアップグレードし項目拡張を実施している場合は、[Enterprise Edition - バージョンアップ手順](../../../products-info/enterprise-edition/version-up/index.md)に従ってバージョンアップを実施してください。
1.  Pleasanter Extensionsの[トライアル](../../../developers-guide/index.md)を実施中の場合は、「Pleasanter Extensionsのトライアルの注意点」を確認してください。
1.  CodeDefiner実行時に/l、/zのパラメータを設定しないでください。
1.  <span class="pl-attention">**ver.1.4.17.0以降でインストーラによるアップデートおよびマージ機能をご利用の際は、[ver.1.4.17.0以降でマージ機能を利用する際の注意事項](https://pleasanter.org/ja/manual/version-up-ver1.4.17.0-caution)を確認してください。**</span>

## 制限事項

1.  CodeDefinerのマージ機能は1.4.8.0以降より利用可能です。
1.  CodeDefinerのマージ機能は、新バージョンで追加および削除されたパラメータを適用します。
1.  バージョンアップ元は1.4.0.0以降が対象です。

## 操作手順

### 1. プリザンターの停止

1.  [Azure Portal](https://portal.azure.com/)に接続します。
1.  App Service を開きます。

    ![Azure Portalの画面。App Serviceを開くところ](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/90ff8944d431483da62410cdf5f90100.png)

1.  作成済みのApp Serviceインスタンスを選択します。
1.  App Serviceを停止します。

### 2. データベースのバックアップ

データベースをバックアップします。**Enterprise Editionにアップグレードし、項目を拡張している場合は必ずバックアップしてください。**  
[Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)

### 3. プリザンターのバックアップ

1.  C:\web\pleasanter_bkフォルダをローカル環境に作成します。
1.  [Kudu](https://docs.microsoft.com/ja-jp/azure/app-service/resources-kudu#access-kudu-for-your-app) にアクセスします。

    1.  App Service の左側のメニューの"開発ツール"から「高度なツール」をクリック

        ![App Serviceの左メニュー。「開発ツール」の中に「高度なツール」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/9e9a929cb8174c9f81ac9a25479890c4.png)

    1.  移動のリンクをクリック

        ![App Serviceの「高度なツール」画面。Kuduへの「移動」リンクがある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/8639e642c6ed4b07b1b86538b8394a9f.png)

    1.  Kudu のヘッダメニューから「Debug console」>「CMD」をクリック

        ![Kuduのヘッダメニュー。「Debug console」の中に「CMD」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/8d9aeb33b8b94c62a787d8adca8360c8.png)

    1.  ディレクトリ一覧から「site」をクリックします。選択後、プロンプトが C:\home\site\となることを確認します。

        ![Kuduのディレクトリ一覧。「site」を選んだ状態](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/1082db49c78b49afbe9ce76636e83f8b.png)

1.  Kudu上のC:\home\site\wwwroot\をダウンロードして、手順3.1でローカル環境に作成したフォルダ配下に配置し解凍します。
1.  **C:\web\pleasanter_bk\wwwroot**を**C:\web\pleasanter_bk\Implem.Pleasanter**にリネームします。

    |変更前|変更後|
    |:--|:--|
    |C:\web\pleasanter\wwwroot|C:\web\pleasanter\Implem.Pleasanter|

### 4. プリザンターの準備

#### 4.1. アプリケーションの準備

1.  [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。
1.  ダウンロードしたzipファイルを解凍しローカル環境のC:\web\配下に解凍します。
1.  **C:\web** ディレクトリ配下の構成が以下のようになっていることを確認してください。

    ```text
    C:\web\pleasanter
    C:\web\pleasanter_bk
    ```

#### 4.2. パッチファイルのダウンロード

1.  [GitHubのリリースページ](https://github.com/Implem/Implem.Pleasanter/releases)から、配置したバージョンと同様のバージョンのParametersPatch.zipをダウンロードします。
1.  ParametersPatch.zipを **C:\web\pleasanter** ディレクトリ配下に配置します。  
    C:\web\pleasanter\ParametersPatch.zip [^1]  

[^1]: ParametersPatch.zipは解凍せずに配置してください。

#### 4.3. パラメータ再設定

C:\web\pleasanter\Implem.CodeDefinerフォルダに移動し、CodeDefinerでパラメータのマージ処理を実行します。

``` bat
> cd C:\web\pleasanter\Implem.CodeDefiner
> dotnet Implem.CodeDefiner.dll merge /b C:\web\pleasanter_bk /i C:\web\pleasanter
```

パラメータのマージ機能については、以下マニュアルページを参照ください。  
[FAQ：パラメータのマージ機能について](../../../FAQ/system-requirements-and-setup/faq-codedefiner-parameters-merge.md)

**パラメータを手動で再設定する場合 [FAQ:パラメータを手動で再設定する手順を知りたい](../../../FAQ/system-requirements-and-setup/faq-merge-parameters.md) を参照ください**

#### 4.4. アプリケーションの配置

1.  手順4.3でパラメータ再設定したローカル環境の最新バージョンモジュールの「C:\web\pleasanter」フォルダに移動します。
1.  「C:\web\pleasanter\Implem.Pleasanter」フォルダを「wwwroot」にリネームします。

    |変更前|変更後|
    |:--|:--|
    |C:\web\pleasanter\Implem.Pleasanter|C:\web\pleasanter\wwwroot|

1.  wwwrootフォルダをzip形式で圧縮し「wwwroot.zip」とします。
1.  「C:\web\pleasanter\Implem.CodeDefiner」フォルダを「CodeDefiner」にリネームします。

    |変更前|変更後|
    |:--|:--|
    |C:\web\pleasanter\Implem.CodeDefiner|C:\web\pleasanter\CodeDefiner|

1.  CodeDefinerフォルダをzip形式で圧縮し「CodeDefiner.zip」とします。
1.  wwwroot.zipとCodeDefiner.zipをKuduのSizeをターゲットにドラッグアンドドロップし、展開されて格納されたことを確認します。

    ![Kuduにwwwroot.zipとCodeDefiner.zipを配置し、展開された状態](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/6a380563ed384537bce6539c052e7624.png)

!!! warning
    念のため、既存のC:\home\site\wwwroot\およびC:\home\site\CodeDefiner\をそれぞれC:\home\site\wwwroot_bk\、C:\home\site\CodeDefiner_bk\などとリネームしてバックアップしたうえで、新バージョンを配置することを推奨します。

### 5. CodeDefinerの実行

1.  Kuduのディレクトリ一覧からCodeDefinerを選択し、プロンプトがC:\home\site\CodeDefinerとなることを確認します。
1.  以下のコマンドを実行して、CodeDefinerを実行します。/l、/zの引数設定は不要です。

    ``` bat
    dotnet Implem.CodeDefiner.dll _rds /p C:\home\site\wwwroot
    ```

1.  実行確認を求められますので、「y」を入力し、++enter++ キーを押して実行してください。実行をキャンセルしたい場合は「n」を入力し、++enter++ キーを押してください。

    ![CodeDefinerの実行画面。実行確認にyを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/527d0a3a72344a3db70d82473662cdff.png)

!!! warning

    Licenseeの表示は環境によって文字化けする可能性があります。

### 6. プリザンターの起動確認

1.  App Serviceを開き、インスタンスを起動します。
1.  ブラウザでプリザンターのログイン画面を開き、ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。

    ![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/0d80470fa83c40bd99c057d2447549e0.png)

!!! warning
    手順3でバックアップしたC:\web\pleasanter_bkは不要な場合は削除してください。保存しておく場合は別フォルダに退避してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.8.0 以降|パラメータのマージ手順追加|

## 関連情報

-   [FAQ：セットアップを自動化した際にCodeDefinerの処理が止まってしまう](../../../FAQ/system-requirements-and-setup/faq-codedefiner-stop.md)
-   [CodeDefinerのコマンド一覧](../../codedefiner/codedefiner-command.md)
