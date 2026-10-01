---
title: プリザンターをAzure App Serviceにサーバレス構成でインストールする
category: プリザンターのインストール
order: '800'
status: ''
parts: ''
urlstring: getting-started-pleasanter-azure
translationKey: getting-started-pleasanter-azure
shortname: プリザンターのインストール,App Serviceにインストール
created: 2021-08-26
updated: 2026-01-13
---

## 概要

Microsoft Azure の App Service と SQL Database を利用しサーバレス構成でプリザンターの動作環境を構築するための手順を示したものです。

| 対象               | 環境・バージョン             |
| ------------------ | :--------------------------- |
| Web                | Microsoft Azure App Service   |
| DB                 | Microsoft Azure SQL Database |
| ランタイムスタック | .NET 10                      |

## 注意事項

1. ver1.4.6以降でのインストール時に、CodeDefinerに引数を指定しないで実行した場合、言語：英語、タイムゾーン：UTCでセットアップされますので、必要に応じて言語とタイムゾーンをご指定ください。
1.ver1.4.5以前をインストールする場合は初回インストール時のCodeDefinerのコマンドが変更されているため、以下ページを参照してください。  
[ver1.4.6以降で初回インストール時のCodeDefinerの手順について](../prerequisites/codedefiner-changed-steps.md)

## 前提条件

1. Azure Portal へのログインが可能であること
1. Microsoft Azure App Service（Windows/.NET 10）が 1 インスタンス準備できている
1. Microsoft Azure SQL Database が 1 インスタンス準備できている
1. Microsoft Azure SQL Database の接続文字列が準備できている
1. Microsoft Azure SQL Database のファイアウォール設定で App Service および PC からの接続が許可されている

## 手順

構築手順は以下の通りです。

1. 事前準備
1. .NETの設定
1. プリザンターのダウンロードおよびパラメータ設定
1. プリザンターの配置
1. CodeDefinerの実行
1. プリザンターの起動確認

## 1. .NET の設定

1. [Azure Portal](https://portal.azure.com/)に接続します。
1. App Service を開きます。
    ![Azure Portal で App Service を開いたところ](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/90ff8944d431483da62410cdf5f90100.png)
1. 作成済みの App Service インスタンスを選択します。
1. 「構成」メニューの「全般設定」を開き、下図の通り設定します。
   ![App Service の「構成」の「全般設定」の画面](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/b1521673e01f4055a29fbc31fdec576c.png)
   ![App Service の「全般設定」の画面。設定項目の続き](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/bcfe86d9950b49a2ba5baf02bc26a08d.png)

    |番号|項目|設定内容|
    |:-:|:--|:--|
    |1|構成 (プレビュー)|クリックして選択します|
    |2|全般設定|クリックして選択します|
    |3|プラットフォーム|64bit|
    |4|FTPの状態|無効|
    |5|Always On|オン（※常時接続と表示されることがあります）|
    |6|スタック設定|クリックして選択します|
    |7|スタック|.NET|
    |8|.NETのバージョン|.NET 10 (LTS)

## 2. プリザンターのダウンロードおよびパラメータ設定

1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。  
   プリザンター1.4.23.3以前をインストールする場合は、[GitHub](https://github.com/Implem/Implem.Pleasanter/releases)から任意のバージョンのzipファイル（例：Pleasanter_1.4.23.3.zip）をダウンロードします。
1. ダウンロードしたzipファイルを解凍します。
1. パラメータファイルを設定します。
   1.  データベースへの接続情報を設定します。  
      「pleasanter\Implem.Pleasanter\App_Data\Parameters\Rds.json」を開き、パラメータを下記の通りに設定し、保存します。

      |パラメータ名|値|説明|
      |:--|:--|:--|
      |Dbms|SQLServer|リレーショナル・データベースに Microsoft Azure SQL Database を使用。|
      |Provider|Azure|リレーショナル・データベースに Microsoft Azure SQL Database を使用。|
      |SaConnectionString|**\*\*\*\***|Microsoft Azure SQL Database の接続文字列。|
      |OwnerConnectionString|**\*\*\*\***|Microsoft Azure SQL Database の接続文字列。|
      |UserConnectionString|**\*\*\*\***|Microsoft Azure SQL Database の接続文字列。|
      |SqlCommandTimeOut|0|SQL コマンドタイムアウト時間を無期限にする。|
      |MinimumTime|3|データベースが識別可能な最小時間単位をミリ秒で指定。本パラメータは変更不可。|
      |DeadlockRetryCount|4|デッドロック発生時の最大再試行回数。|
      |DeadlockRetryInterval|1000|デッドロック発生時に再試行を行うまでの間隔。|
      |DisableIndexChangeDetection|true|バージョンアップ時にデータベースのインデックスの差異を検出しない。|

   1.  サービス情報を設定してください。  
       ご利用のバージョンで設定内容が異なります。
      「pleasanter\Implem.Pleasanter\App_Data\Parameters\Service.json」を開き、パラメータを下記の通りに設定し、保存します。

      ### ver.1.4.5まで

         |パラメータ名|値|説明|
         |:--|:--|:--|
         |Name|(データベース名)|Azure で作成したデータベース名を設定|
         |TimeZoneDefault|Tokyo Standard Time|既定のタイムゾーンをWindowsで有効な名前で指定(※1)|

      (※1) タイムゾーンは以下マニュアルページを参照ください。
   [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

      ### ver.1.4.6以降

         |パラメータ名|値|説明|
         |:--|:--|:--|
         |Name|(データベース名)|Azure で作成したデータベース名を設定|     

## 3. プリザンターの配置

1. App Service にてインスタンスを停止します。
1. [Kudu](https://docs.microsoft.com/ja-jp/azure/app-service/resources-kudu#access-kudu-for-your-app) にアクセスします。
   1. App Service の左側のメニューの"開発ツール"から「高度なツール」をクリック
     ![App Service の左メニューの「開発ツール」。「高度なツール」がある](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/9e9a929cb8174c9f81ac9a25479890c4.png)
   2. 移動のリンクをクリック
      ![高度なツール（Kudu）の画面。「移動」のリンクがある](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/8639e642c6ed4b07b1b86538b8394a9f.png)
   3. Kudu のヘッダメニューから「Debug console」>「CMD」をクリック
      ![Kudu のヘッダメニュー。「Debug console」から「CMD」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/8d9aeb33b8b94c62a787d8adca8360c8.png)
   4. ディレクトリ一覧から「site」をクリックします。選択後、プロンプトが "C:\home\site" になったことを確認します。（ご利用ユーザによってはD:\home\siteの場合もあります。その場合は適宜読み替えてください。）
      ![Kudu の Debug console。ディレクトリ一覧から「site」を選んだ状態](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/1082db49c78b49afbe9ce76636e83f8b.png)

1. 「2. プリザンターのダウンロードおよびパラメータ設定」で準備したプリザンターファイルをApp Serviceにアップロードします。
   1. 「pleasanter」フォルダに移動します。
   2. 「Implem.Pleasanter」フォルダを「wwwroot」にリネームします。
   3. wwwroot フォルダを zip 形式で圧縮し「wwwroot.zip」とします。
   4. 「Implem.CodeDefiner」フォルダを[CodeDefiner](../../codedefiner/codedefiner-command.md)にリネームします。
   5. CodeDefiner フォルダを zip 形式で圧縮し「CodeDefiner.zip」とします。
   6. wwwroot.zip と CodeDefiner.zip を Kudu の Size をターゲットにドラッグアンドドロップし、展開されて格納されたことを確認します。
      ![Kudu の Debug console。wwwroot.zip と CodeDefiner.zip が展開されて格納された状態](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/6a380563ed384537bce6539c052e7624.png)

## 4. CodeDefiner の実行

1. Kudu のディレクトリ一覧から CodeDefiner を選択し、 プロンプトが C:\home\site\CodeDefiner となることを確認します。
2. 以下のコマンドを実行して、CodeDefinerを実行します。  
※下記コマンドは初回インストール時にのみ実行します。

```
dotnet Implem.CodeDefiner.dll _rds /p C:\home\site\wwwroot /l "<言語>" /z "<タイムゾーン>"
```

|引数|設定例|説明|
|:--|:--|:--|
|/l|ja|Service.jsonのDefaultLanguageの値を書き換えます(※1)|
|/z|Tokyo Standard Time|Service.jsonのTimeZoneDefaultの値を書き換えます(※1)|  

(※1) 言語、タイムゾーンは以下マニュアルページを参照ください。
[FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

日本語環境でご利用する場合は以下コマンドとなります。

```
dotnet Implem.CodeDefiner.dll _rds /p C:\home\site\wwwroot /l "ja" /z "Tokyo Standard Time"
```

## 5. プリザンターの起動確認

1. App Serviceにてインスタンスを起動します。

1. ブラウザでプリザンターのログイン画面を開き、「ログインID: Administrator」、「初期パスワード: pleasanter」を入力し、「ログイン」ボタンをクリックします。
![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/5477647dc121413190827affdc7fa1ff.png)

1. ログイン後に「Administrator」ユーザーのパスワード変更を求められるので、任意のパスワードを入力し、「変更」ボタンをクリックします。  
![初回ログイン後に表示される、Administrator のパスワード変更画面](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/d57262564d8e49568553a84b273d3797.png)