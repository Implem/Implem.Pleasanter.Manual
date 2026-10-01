---
title: PostgreSQL14で動作しているプリザンターをPostgreSQL15の環境へ移行したい。
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-migrate-postgresql14-based-to-postgresql15-based
translationKey: faq-migrate-postgresql14-based-to-postgresql15-based
shortname: ''
created: 2024-02-13
updated: 2025-04-10
---

## 回答

旧環境（PostgreSQL14）のリストア作業と新環境（PostgreSQL15）のプリザンターインストール作業を組み合わせます。

---

## 概要

こちらの手順は下記の内容が前提となっております。

-   PostgreSQLのバージョン14がインストールされている環境を **旧サーバ** 、バージョン15がインストールされている環境を **新サーバ** と呼びます。
-   新サーバはOSのインストールまで完了していること。**<span class="pl-attention">※プリザンター、PostgreSQLはインストールしていないこと。</span>**
-   旧サーバ、新サーバともに接続可能な作業用端末があること。※この手順ではWindowsの端末を想定しています。
-   旧サーバはユーザマニュアルに記載の手順で導入されていること。※publicスキーマにデータベース(Implem.Pleasanter)が存在すること。

## 制限事項

下記手順に従いpublicスキーマにて作成したデータベース(Implem.Pleasanter)を新環境へリストアしても、スキーマは自動で変更されません。1.3.44.0以降のバージョンでインストール用のCodeDefinerを実行した時同様、publicスキーマ以外にデータベース(Implem.Pleasanter)を構築したい場合はプリザンターのサイトパッケージまたはレコードのインポート/エクスポート機能を利用してデータ移行を行うか、リストアの実施後に新環境のDBのロール・スキーマを変更してください。

### 環境情報

手順に記載されている旧サーバ、新サーバの環境情報は以下の通りです。※上記の前提に記載の通り、新サーバは手順実施前はOSのインストールまでが完了していることとします。

#### 旧サーバ

-   OS: AlmaLinux 9.2
-   DB: PostgreSQL14
-   Pleasanter: 1.3.43.0

#### 新サーバ

-   OS: AlmaLinux 9.2
-   DB: PostgreSQL15
-   Pleasanter: 1.3.48.0 

## 操作手順

1. 旧サーバで以下のコマンドでPostgreSQLのバックアップを取得します。

    ``` bash
    pg_dumpall --roles-only > /backup/Implem.Pleasanter_role.dump
    pg_dump -Fc Implem.Pleasanter > /backup/Implem.Pleasanter.dump
    ```

2. 新サーバに上記1で取得したバックアップファイルをコピーします。この手順では新サーバに以下のように「/backup」ディレクトリにコピーすることとします。

    -   /backup/Implem.Pleasanter_role.dump
    -   /backup/Implem.Pleasanter.dump

3. 旧サーバのプリザンターのパラメータが格納されている「/web/pleasanter/Implem.Pleasanter/App_Data/Parameters」ディレクトリを作業用端末にコピーします。この手順では以下のように「C:\backup」フォルダにコピーすることとします。

    -   C:\backup\Parameters

4. 作業用端末で対象バージョン(1.3.48.0)のモジュールをダウンロードします。

5. 上記4でダウンロードしたモジュール(zip)を展開します。この手順では「C:\work」フォルダに展開することとします。

6. 以下の各フォルダ配下のパラメータファイルを比較し、設定値をマージします。※WinMerge等のツールで比較、マージを実施することを推奨します。

    -   上記3の「C:\backup\Parameters」フォルダ
    -   上記5の「C:\work\pleasanter\Implem.Pleasanter\App_Data\Parameters」フォルダ　※こちらのフォルダ配下のファイルにマージします。

7. 新サーバで下記ユーザマニュアルを参考に「PostgreSQLのセットアップ」まで実施します。　※postgresユーザのパスワードは旧サーバと同じものを想定しています。

    -   [プリザンターをAlmaLinuxにインストールする](../../setup/installation/install-manually/getting-started-pleasanter-almalinux.md)

8. 新サーバで下記コマンドを実行してデータベースを作成します。
    ```
    psql -U postgres -c 'create database "Implem.Pleasanter";'
    psql -U postgres -c 'create extension if not exists pg_trgm;'
    ```

9.  上記2でコピーしてきたバックアップファイルを使用して、下記コマンドでロール、データベースを復元します。
    ```
    psql -f /backup/Implem.Pleasanter_role.dump
    pg_restore -d Implem.Pleasanter /backup/Implem.Pleasanter.dump
    ```

10. 上記6で整理したモジュールを新サーバに配置します。配置後のイメージは以下の通りです。※各ディレクトリ権限は適宜変更してください。

    -   /web/pleasanter/Implem.Pleasanter
    -   /web/pleasanter/Implem.CodeDefiner

11. 新サーバで下記ユーザマニュアルを参考に「CodeDefinerの実行」から後続の手順を実行します。

    -   [プリザンターをAlmaLinuxにインストールする](../../setup/installation/install-manually/getting-started-pleasanter-almalinux.md)

12. 新サーバ上でプリザンターが起動することを確認します。