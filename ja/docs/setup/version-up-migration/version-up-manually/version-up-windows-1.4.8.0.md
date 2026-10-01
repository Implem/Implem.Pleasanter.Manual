---
title: 1.4.8.0以降のバージョンアップ手順(Windows)
category: バージョンアップ
order: '100'
status: ''
parts: ''
urlstring: version-up-windows-1.4.8.0
translationKey: version-up-windows-1.4.8.0
shortname: バージョンアップ手順,Windowsのバージョンアップ手順
created: 2024-08-29
updated: 2026-01-13
---

**<span class="pl-attention">プリザンター1.5以降で、DBにSQL Serverを使用する場合は、必ず以下のマニュアルを確認してください。</span>**  
**[プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項](../../installation/prerequisites/sqlserver-connection-string-v15.md)**

## 概要

Windowsで運用しているプリザンターver1.4.8.0以降のバージョンアップ手順です。

## 注意事項

1. 現在プリザンター 1.4を利用されていて、プリザンター1.5へバージョンアップする場合は[Windows/Windows Serverにインストールしたプリザンター 1.4をプリザンター 1.5へ移行する手順](../migration/migrate-to-pleasanter-windows.md)でプリザンター1.5へ移行してください。
1. 現在運用中のパラメータファイルを最新バージョンに上書きコピーしないでください。最新バージョンで新たに追加したパラメータが失われ、プリザンターが起動しない恐れがあります。
1. Enterprise Editionにアップグレードし項目拡張を実施している場合は、[Enterprise Edition - バージョンアップ手順](../../../products-info/enterprise-edition/version-up/index.md)に従ってバージョンアップを実施してください。
1. Pleasanter Extensionsの[トライアル](../../../developers-guide/index.md)を実施中の場合は、「Pleasanter Extensionsのトライアルの注意点」を確認してください。
1.CodeDefiner実行時に/l、/zのパラメータを設定しないでください。
1. <span class="pl-attention">**ver.1.4.17.0以降でインストーラによるアップデートおよびマージ機能をご利用の際は、[ver.1.4.17.0以降でマージ機能を利用する際の注意事項](https://pleasanter.org/ja/manual/version-up-ver1.4.17.0-caution)を確認してください。**</span>

## 制限事項

1. CodeDefinerのマージ機能は1.4.8.0以降より利用可能です。
1. CodeDefinerのマージ機能は、新バージョンで追加および削除されたパラメータを適用します。
1. バージョンアップ元は1.4.0.0以降が対象です。

## 手順

バージョンアップ手順は以下の通りです。
1. プリザンターの停止
1. データベースのバックアップ
1. プリザンターのバックアップ
1. プリザンターの準備
   1. アプリケーションの準備
   1. パッチファイルのダウンロード
   1. パラメータ再設定
1. CodeDefinerの実行
1. プリザンターの起動確認

## 1.プリザンターの停止

1. 「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS)マネージャー」を起動してください。

1.  左ペインより「サーバー名」を選択します。右ペインの「停止」をクリックして、IISを停止してください。
![IISマネージャーの画面。右ペインの「停止」でIISを停止する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/033a9ee7aa0841369709641c7d94b2bb.png)

## 2. データベースのバックアップ

データベースをバックアップします。**Enterprise Editionにアップグレードし、項目を拡張している場合は必ずバックアップしてください**
    [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)

## 3. プリザンターのバックアップ

既存の`C:\web\pleasanter\`を`C:\web\pleasanter_bk\`などとリネームしてバックアップします。

## 4. プリザンターの準備

### 1. アプリケーションの準備

1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。
1. ダウンロードしたzipファイルを解凍しローカルPCのC:\web\配下に解凍します。  
`C:\web\` ディレクトリ配下の構成が以下のようになっていることを確認してください。
   C:\web\pleasanter
   C:\web\pleasanter_bk

### 2. パッチファイルのダウンロード

1. [GitHubのリリースページ](https://github.com/Implem/Implem.Pleasanter/releases)から、配置したバージョンと同様のバージョンのParametersPatch.zipをダウンロードします。
1. ParametersPatch.zipを `C:\web\pleasanter\` ディレクトリ配下に配置します。  
C:\web\pleasanter\ParametersPatch.zip  
※ParametersPatch.zipは解凍せずに配置してください。

### 3. パラメータ再設定

C:\web\pleasanter\Implem.CodeDefiner\フォルダに移動し、CodeDefinerでパラメータのマージ処理を実行します。

```
> cd C:\web\pleasanter\Implem.CodeDefiner
> dotnet Implem.CodeDefiner.dll merge /b C:\web\pleasanter_bk /i C:\web\pleasanter
```

パラメータのマージ機能については、以下マニュアルページを参照ください。
[FAQ：パラメータのマージ機能について](../../../FAQ/system-requirements-and-setup/faq-codedefiner-parameters-merge.md)

**パラメータを手動で再設定する場合
[FAQ:パラメータを手動で再設定する手順を知りたい](../../../FAQ/system-requirements-and-setup/faq-merge-parameters.md)  を参照ください**

## 5. CodeDefinerの実行

コマンドプロンプトまたはPowerShellを起動し、Implem.CodeDefinerフォルダーに移動しCodeDefinerを実行します。/l、/zの引数設定は不要です。

```
> cd C:\web\pleasanter\Implem.CodeDefiner
> dotnet Implem.CodeDefiner.dll _rds
```

実行確認を求められますので、「y」を入力し、Enterキーを押して実行してください。実行をキャンセルしたい場合は「n」を入力し、Enterキーを押してください。
![WindowsでのCodeDefinerの実行画面。実行確認にyを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/f233abe822734d44a1f1e4bf95aa82a2.png)
※Licenseeの表示は環境によって文字化けする可能性があります。

## 6. プリザンターの起動確認

1. 「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS）マネージャー」を起動します。

1.  左ペインより「サーバー名」を選択します。右ペインの「開始」をクリックして、IISを開始します。
![IISマネージャーの画面。右ペインの「開始」でIISを開始する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/1fb50733a47b423591b1490ba1c8a272.png)

1. 開始後、左ペインよりサイト-「Default Web Site」を選択し、右ペインの「*.80(http)参照」をクリックし、プリザンターを起動します。
![IISマネージャー。「Default Web Site」の「*.80(http)参照」でプリザンターを開く](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/5be4e5794d5941d2b31a51f81a26e0a4.png)

1. ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。
![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/0d80470fa83c40bd99c057d2447549e0.png)

※手順3でバックアップしたC:\web\pleasanter_bkは不要な場合は削除してください。保存しておく場合は別フォルダに退避してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.8.0 以降|パラメータのマージ手順追加|

## 関連情報

[FAQ：セットアップを自動化した際にCodeDefinerの処理が止まってしまう](../../../FAQ/system-requirements-and-setup/faq-codedefiner-stop.md)  
[CodeDefinerのコマンド一覧](../../codedefiner/codedefiner-command.md)  
