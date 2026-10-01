---
title: プリザンターのバージョンアップ手順(Azure App Service)
category: バージョンアップ
order: '1200'
status: ''
parts: ''
urlstring: version-up-azure
translationKey: version-up-azure
shortname: バージョンアップ手順,App Serviceのバージョンアップ手順
created: 2023-04-14
updated: 2026-01-13
---

## 概要

Azure App Serviceで運用しているプリザンターのバージョンアップ手順です。

## 注意事項

1. 現在運用中のパラメータファイルを最新バージョンに上書きコピーしないでください。最新バージョンで新たに追加したパラメータが失われ、プリザンターが起動しない恐れがあります。
1. Enterprise Editionにアップグレードし項目拡張を実施している場合は、[Enterprise Edition - バージョンアップ手順](../../../products-info/enterprise-edition/version-up/index.md)に従ってバージョンアップを実施してください。
1. Pleasanter Extensionsの[トライアル](../../../developers-guide/index.md)を実施中の場合は、「Pleasanter Extensionsのトライアルの注意点」を確認してください。
1.CodeDefiner実行時に/l、/zのパラメータを設定しないでください。

## 前提条件

1. プリザンター 1.3 以前のバージョンから、プリザンター 1.4 以降へバージョンアップする場合、[.NET8のインストール](../../installation/install-dotnet/index.md)が必要です。

## 手順

バージョンアップ手順は以下の通りです。
1. データベースのバックアップ
1. パラメータファイルのバックアップ
1. プリザンターの準備
   1. アプリケーションの準備
   1. パラメータ再設定
   1. 拡張機能の再設定
1. プリザンターの配置
   1. プリザンターの停止
   1. アプリケーションの配置
1. CodeDefinerの実行
1. プリザンターの起動確認

## 1. データベースのバックアップ

データベースをバックアップします。**Enterprise Editionにアップグレードし、項目を拡張している場合は必ずバックアップしてください**
    [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)

## 2. パラメータファイルのバックアップ

1. パラメータファイルをバックアップします。このバックアップは手順3.2.で使用します。パラメータファイルはマニュアル通りにセットアップした場合、C:\home\sites\wwwroot\Implem.Pleasanter\App_Data\Parameters\配下のjsonファイルとなります。
1. **拡張機能を利用していない場合は本手順は不要です。** 拡張機能で設定したパラメータファイルをバックアップします。このバックアップは手順3.3.で使用します。拡張機能で設定したファイルはマニュアル通りにセットアップした場合、C:\home\sites\wwwroot\Implem.Pleasanter\App_Data\Parameters\配下にある以下サブフォルダ内のファイルとなります。

    |サブフォルダ名|拡張機能名|備考|
    |:---|:---|:---|
    |CustomDefinitions|[拡張項目](../../../developers-guide/extended-features/extended-column.md)|組織、グループ、ユーザに項目を追加した際に生成されるフォルダ|
    |ExtendedFields|[拡張フィールド](../../../developers-guide/extended-features/extended-fields.md)||
    |ExtendedHtmls|[拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)||
    |ExtendedNavigationMenus|[拡張ナビゲーションメニュー](../../../developers-guide/extended-features/extended-navigationmenus.md)||
    |ExtendedScripts|[拡張スクリプト](../../../developers-guide/extended-features/extended-script.md)||
    |ExtendedServerScripts|[拡張サーバスクリプト](../../../developers-guide/extended-features/extended-server-script.md)||
    |ExtendedSqls|[拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)||
    |ExtendedStyles|[拡張スタイル](../../../developers-guide/extended-features/extended-style.md)||

## 3. プリザンターの準備

### 1. アプリケーションの準備

1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。
1. ダウンロードしたzipファイルを解凍します。

### 2. パラメータ再設定

手順3.1.で準備した最新バージョンモジュールのパラメータファイルに対して、現在設定済みの内容を反映します。[WinMerge](https://winmergejp.bitbucket.io/)などのファイル比較・マージツールを利用して最新バージョンモジュールのパラメータファイルと手順2.で取得したバックアップファイルのパラメータファイルを比較しながら最新バージョンモジュールのパラメータファイルを修正します。  
**Service.jsonのTimeZoneDefaultが正しい値か確認してください。TimeZoneDefaultにはPleasanterをインストールするサーバのOSで有効なタイムゾーンを設定してください。（Windowsなら"Tokyo Standard Time"など、Linuxなら"Asia/Tokyo"など）**  
[FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)    

### 3. 拡張機能の再設定

**拡張機能を利用していない場合は本手順は不要です。** 手順3.1で準備した最新バージョンモジュールの拡張機能用パラメータファイルに対して、現在設定済みの内容を反映します。[WinMerge](https://winmergejp.bitbucket.io/)などのファイル比較・マージツールを利用して最新バージョンモジュールの拡張機能用パラメータファイルと手順2.で取得したバックアップファイルの拡張機能用パラメータファイルを比較しながら最新バージョンモジュールの拡張機能用パラメータファイルを修正します。

## 4. プリザンターの配置

### 1. プリザンターの停止

1. [Azure Portal](https://portal.azure.com/)に接続します。
2. App Service を開きます。
    ![Azure Portalの画面。App Serviceを開くところ](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/90ff8944d431483da62410cdf5f90100.png)
3. 作成済みの App Service インスタンスを選択します。
4. App Serviceを停止します。

### 2. アプリケーションの配置

1. [Kudu](https://docs.microsoft.com/ja-jp/azure/app-service/resources-kudu#access-kudu-for-your-app) にアクセスします。
   1. App Service の左側のメニューの"開発ツール"から「高度なツール」をクリック
     ![App Serviceの左メニュー。「開発ツール」の中に「高度なツール」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/9e9a929cb8174c9f81ac9a25479890c4.png)
   2. 移動のリンクをクリック
      ![App Serviceの「高度なツール」画面。Kuduへの「移動」リンクがある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/8639e642c6ed4b07b1b86538b8394a9f.png)
   3. Kudu のヘッダメニューから「Debug console」>「CMD」をクリック
      ![Kuduのヘッダメニュー。「Debug console」の中に「CMD」がある](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/8d9aeb33b8b94c62a787d8adca8360c8.png)
   4. ディレクトリ一覧から「site」をクリックします。選択後、プロンプトが C:\home\site\となることを確認します。
      ![Kuduのディレクトリ一覧。「site」を選んだ状態](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/1082db49c78b49afbe9ce76636e83f8b.png)
2. 手順3.2.でパラメータ再設定した最新バージョンモジュールの「pleasanter」フォルダに移動します。
3. 「Implem.Pleasanter」フォルダを「wwwroot」にリネームします。
4. wwwroot フォルダを zip 形式で圧縮し「wwwroot.zip」とします。
5. 「Implem.CodeDefiner」フォルダを[CodeDefiner](../../codedefiner/codedefiner-command.md)にリネームします。
6. CodeDefiner フォルダを zip 形式で圧縮し「CodeDefiner.zip」とします。
7. wwwroot.zip と CodeDefiner.zip を Kudu の Size をターゲットにドラッグアンドドロップし、展開されて格納されたことを確認します。
   ![Kuduにwwwroot.zipとCodeDefiner.zipを配置し、展開された状態](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/6a380563ed384537bce6539c052e7624.png)
※念の為、既存のC:\home\site\wwwroot\およびC:\home\site\CodeDefiner\をそれぞれC:\home\site\wwwroot_bk\、C:\home\site\CodeDefiner_bk\などとリネームしてバックアップしたうえで、新バージョンを配置することを推奨します。  

## 5. CodeDefinerの実行

1. Kudu のディレクトリ一覧から CodeDefiner を選択し、プロンプトが C:\home\site\CodeDefiner となることを確認します。
2. 以下のコマンドを実行して、CodeDefinerを実行します。/l、/zの引数設定は不要です。

```
dotnet Implem.CodeDefiner.dll _rds /p C:\home\site\wwwroot
```

## 6. プリザンターの起動確認

1. App Serviceを開き、インスタンスを起動します。
1. ブラウザでプリザンターのログイン画面を開き、ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。
![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/0d80470fa83c40bd99c057d2447549e0.png)
