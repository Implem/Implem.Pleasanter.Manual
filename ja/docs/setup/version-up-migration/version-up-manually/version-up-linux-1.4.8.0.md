---
title: 1.4.8.0以降のバージョンアップ手順(Linux)
category: バージョンアップ
order: '300'
status: ''
parts: ''
urlstring: version-up-linux-1.4.8.0
translationKey: version-up-linux-1.4.8.0
shortname: バージョンアップ手順,Linuxのバージョンアップ手順
created: 2024-08-27
updated: 2026-01-13
---

## 概要

Linux系OSで運用しているプリザンターver1.4.8.0以降のバージョンアップ手順です。

## 注意事項

1. 現在運用中のパラメータファイルを最新バージョンに上書きコピーしないでください。最新バージョンで新たに追加したパラメータが失われ、プリザンターが起動しない恐れがあります。
1. Enterprise Editionにアップグレードし項目拡張を実施している場合は、[Enterprise Edition - バージョンアップ手順](../../../products-info/enterprise-edition/version-up/index.md)に従ってバージョンアップを実施してください。
1. Pleasanter Extensionsの[トライアル](../../../developers-guide/index.md)を実施中の場合は、「Pleasanter Extensionsのトライアルの注意点」を確認してください。
1.CodeDefiner実行時に/l、/zのパラメータを設定しないでください。
1. <span class="pl-attention">**ver.1.4.17.0以降でインストーラによるアップデートおよびマージ機能をご利用の際は、[ver.1.4.17.0以降でマージ機能を利用する際の注意事項](https://pleasanter.org/ja/manual/version-up-ver1.4.17.0-caution)を確認してください。**</span>

## 制限事項

1. CodeDefinerのマージ機能は1.4.8.0以降より利用可能です。
1. CodeDefinerのマージ機能は、新バージョンで追加および削除されたパラメータを適用します。
1. バージョンアップ元は1.4.0.0以降が対象です。

## 前提条件

1. プリザンターを起動するユーザが登録されていること。手順の中で記載している **<プリザンターを起動するユーザ>** はこのユーザを指します。
1. 本手順では.NETを /usr/local/bin にインストールする場合として説明します。同一環境に複数バージョンの.NETが必要などの理由で.NETを異なるディレクトリにインストールする場合は、CodeDefinerの実行時やPleasanterサービス用スクリプトの作成でExecStartに指定するディレクトリをインストール先に合わせて変更してください。

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

以下コマンドを実行して、プリザンターを停止します。

```
sudo systemctl stop pleasanter
```

## 2. データベースのバックアップ

データベースをバックアップします。**Enterprise Editionにアップグレードし、項目を拡張している場合は必ずバックアップしてください**
    [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)

## 3. プリザンターのバックアップ

既存の**/web/pleasanter/**を**/web/pleasanter_bk/**などとリネームしてバックアップします。

## 4. プリザンターの準備

### 1. アプリケーションの準備

1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。
1. ダウンロードしたzipファイルを解凍し/web/配下に解凍します。  
**/web/** ディレクトリ配下の構成が以下のようになっていることを確認してください。
   /web/pleasanter
   /web/pleasanter_bk
1. 以下コマンドを実行して、pleasanterディレクトリ配下の所有者をあらかじめ決めたプリザンターを起動するユーザに変更します。

    ```
    sudo chown -R <プリザンターを起動するユーザ> /web/pleasanter
    ```

### 2. パッチファイルのダウンロード

1. [GitHubのリリースページ](https://github.com/Implem/Implem.Pleasanter/releases)から、配置したバージョンと同様のバージョンのParametersPatch.zipをダウンロードします。
1. ParametersPatch.zipを **/web/pleasanter/** ディレクトリ配下に配置します。  
 /web/pleasanter/ParametersPatch.zip  
※ParametersPatch.zipは解凍せずに配置してください。

### 3. パラメータ再設定

/web/pleasanter/Implem.CodeDefinerディレクトリに移動し、CodeDefinerでパラメータのマージ処理を実行します。

```
> cd /web/pleasanter/Implem.CodeDefiner
> sudo -u <プリザンターを起動するユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll merge /b /web/pleasanter_bk /i /web/pleasanter
```
パラメータのマージ機能については、以下マニュアルページを参照ください。
[FAQ：パラメータのマージ機能について](../../../FAQ/system-requirements-and-setup/faq-codedefiner-parameters-merge.md)

**パラメータを手動で再設定する場合
[FAQ:パラメータを手動で再設定する手順を知りたい](../../../FAQ/system-requirements-and-setup/faq-merge-parameters.md)  を参照ください**

## 5. CodeDefinerの実行

以下コマンドを実行して、あらかじめ決めたプリザンターを起動するユーザでCodeDefinerを実行します。/l、/zの引数設定は不要です。

```
cd /web/pleasanter/Implem.CodeDefiner
sudo -u <プリザンターを起動するユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds
```

実行確認を求められますので、「y」を入力し、Enterキーを押して実行してください。実行をキャンセルしたい場合は「n」を入力し、Enterキーを押してください。
![Linuxでの CodeDefiner の実行画面。実行確認にyを入力する](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/679891e64df748fc869c47f482f542ea.png)
※Licenseeの表示は環境によって文字化けする可能性があります。

## 6. プリザンターの起動確認

1. 以下コマンドを実行して、プリザンターを起動します。

    ```
    sudo systemctl start pleasanter
    ```

2. ブラウザでプリザンターのログイン画面を開き、ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。
    ![「ヘルプ」－「バージョン」で表示したプリザンターのバージョン情報](https://pleasanter.org/files/images/ja/setup/version-up-migration/version-up-manually/assets/0d80470fa83c40bd99c057d2447549e0.png)

※手順3でバックアップした/web/pleasanter_bkは不要な場合は削除してください。保存しておく場合は別フォルダに退避してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.8.0 以降|パラメータのマージ手順追加|

## 関連情報

[FAQ：セットアップを自動化した際にCodeDefinerの処理が止まってしまう](../../../FAQ/system-requirements-and-setup/faq-codedefiner-stop.md)
[CodeDefinerのコマンド一覧](../../codedefiner/codedefiner-command.md)
