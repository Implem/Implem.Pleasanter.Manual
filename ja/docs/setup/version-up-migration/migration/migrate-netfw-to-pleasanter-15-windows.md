---
title: Windows/Windows Serverにインストールした.netFramework版プリザンターをプリザンター 1.5へ移行する手順
category: 移行
order: '300'
status: ''
parts: ''
urlstring: migrate-netfw-to-pleasanter-15-windows
shortname: ''
created: 2026-08-24
updated: 2026-08-24
---

## 概要
Windows Serverにインストールされているプリザンターをプリザンター 1.5に移行するための手順です。

|対象|移行前|移行後|
|---|---|---|
|OS|Windows/Windows Server|Windows/Windows Server|
|DB|SQL Server|SQL Server|
|Webサーバ|IIS|IIS|
|Platform|.net Framework4.7/4.8|.NET 10.0|
|Pleasanter|プリザンター 0.50以前|プリザンター 1.5|

## 注意事項
1. 本手順を実施する前にシステムのバックアップおよびデータベースのバックアップを取得するようにしてください。
1. 移行元の環境の設定ファイル(C:\inetpub\wwwroot\pleasanter\App_Data\Parametersフォルダ配下)を編集している場合、移行先の環境へ上書きコピーしないでください。そのまま上書きすると**新しく追加になったパラメータが失われる**可能性がありますので、WinMerge等の差分ツールを使用して、変更部分のみを新しいパラメータファイルにマージしてください。この手順ではWinMergeを使用します。

## 事前確認
Windows/Windows Serverにインストールしているプリザンターのバージョンを確認します。

1. プリザンターへログインします。
1. 画面右上にある「ヘルプ」より「バージョン」をクリックします。
1. バージョンが「0.50.〇.〇（または0.49.〇.〇）」であることを確認します。

## 事前準備
#### 使用ツール
1. WinMergeがインストールされていること。下記ページからダウンロードできます。  
　https://winmergejp.bitbucket.io/  

#### データベースのバックアップ
1. 「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS)マネージャー」を起動してください。

1. 左ペインでサーバ名を選択し、右ペインの「停止」をクリックし、IISを停止してください。
![IISマネージャーの画面。右ペインの「停止」でIISを停止する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/79ffe4e682fc49c9abe8be89508b4e63.png)

1. プリザンターのデータベースのバックアップを取得してください。  
[プリザンターのDBデータを定期的にバックアップしたい（SQL Server）](../../../FAQ/backup-restore/faq-backup-schedule.md)

<!--install-dotnet-10-->

## プリザンター 1.5のダウンロード
1. 以下のURLへアクセスしてください。  
　https://pleasanter.org/dlcenter  

1. 「プリザンター 1.5 Community Edition」のダウンロードリンクより、プリザンターをダウンロードしてください。

## モジュールの配置
1. ダウンロードしたプリザンターのモジュールを「C:\web」フォルダに展開してください。

1. WinMergeを起動し、以下の2つのフォルダを比較してください。  
　①C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters  
　②C:\inetpub\wwwroot\pleasanter\App_Data\Parameters  

![WinMergeで新旧のParametersフォルダを比較した画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/2369c12c4d21480c8f48328989a55a62.png)  

1. 上記①のParametersフォルダ配下の各パラメータファイルを上記②のParametersフォルダ配下のものと比較しながら修正してください。
<span class="pl-attention">※「Extended○○」といったフォルダ内部のJSONファイルは、拡張機能を使っていない場合は変更不要です。</span>  

![WinMergeでパラメータファイルの中身を比較しながら修正する画面](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/589991949bb34f99bb7968937f6a2eb0.png)

パラメータを修正する際、以下のパラメータは移行元のものに合わせて修正する必要がございます。Dbmsは"SQLServer"とし、TimeZoneは"Tokyo Standard Time"に変更してください。

Rds.json

```
"Dbms": "SQLServer"
"TimeZoneInfo": "Tokyo Standard Time"
```

Service.json
```
"TimeZoneDefault": "Tokyo Standard Time"
```

## CodeDefinerの実行
1.コマンドプロンプトを起動し、以下のコマンドを実行してください。
```
cd C:\web\pleasanter\Implem.CodeDefiner
dotnet Implem.CodeDefiner.dll _rds
```

## プリザンターの起動
1. IISマネージャーを起動し、左ペインより移行前のプリザンターの仮想ディレクトリ（標準では、サーバー名 > サイト > Default Web Site > pleasanter）を選択し、右ペインの「基本設定」をクリックしてください。
![IISマネージャー。プリザンターの仮想ディレクトリを選び「基本設定」を開く](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/7fcd209f0cc94d31b4cb63abbd0d761d.png)  

1. 物理パスを「C:\web\pleasanter\Implem.Pleasanter」に編集し、「OK」をクリックしてください。
![基本設定のダイアログ。物理パスを新しいフォルダに編集する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/0f564467a911499cb73a84d643130a28.png)  

1. 左ペインよりサーバー名 > アプリケーションプールを選択し、更に中央ペインの「Default App Pool」を選択し、右ペインの「基本設定」をクリックしてください。
![IISマネージャーのアプリケーションプール一覧。「Default App Pool」を選ぶ](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/b0d96c97e3b74d10b9f7b2c313838b67.png)

1. 「.Net CLR バージョン」を「マネージドコードなし」を選択し、「OK」をクリックしてください。
![アプリケーションプールの基本設定。「.Net CLR バージョン」を選ぶ](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/1c29fb8bbca74307912728bf09709a6e.png)

1. IISマネージャーを起動し、IISを起動してください。
![IISマネージャーの画面。右ペインでIISを起動する](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/11e9e5a79cd2469ca3d38f503a1a9e11.png)

1. ブラウザを起動し、プリザンターへログインできることを確認してください。