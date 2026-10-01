---
title: MySQLに関連するマニュアルを確認したい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-mysql-manual-list
translationKey: faq-mysql-manual-list
shortname: ''
created: 2024-09-18
updated: 2025-02-12
---

## 回答

MySQLに関する記述は以下のマニュアルを参照してください。マニュアルは順次更新しており、公開に併せて本FAQも更新いたします。

---

## 制限事項

1.  MySQLはバージョン1.4.9.0以降で使用できます。バージョン1.4.9.0より前のプリザンターはMySQLに対応していません。また、バージョン1.4.9.0に存在するMySQL関連の不具合が後のバージョンで解消されていますので、可能な限り最新のバージョンのプリザンターをご利用ください。詳細は後述の「対応バージョン」を確認してください。

## MySQLに関連するマニュアルへのリンク

### プリザンターのインストール(インストーラ)

[インストーラでプリザンターをWindowsにインストールする](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-windows.md)
[インストーラでプリザンターをUbuntuにインストールする](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-ubuntu.md)
[インストーラでプリザンターをAlmaLinuxにインストールする](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)
[インストーラでプリザンターをRed Hat Enterprise Linux 8にインストールする](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-rhel-8.md)
[インストーラでプリザンターをRed Hat Enterprise Linux 9.7/10.1にインストールする](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-rhel9.md)

### プリザンターのインストール

[プリザンターをWindowsにインストールする際の事前準備](../../setup/installation/install-manually/getting-preparation-pleasanter-windows.md)
[プリザンターをWindowsにインストールする](../../setup/installation/install-manually/getting-started-pleasanter-windows.md)
[プリザンターをUbuntuにインストールする](../../setup/installation/install-manually/getting-started-pleasanter-ubuntu.md)
[プリザンターをAlmaLinuxにインストールする](../../setup/installation/install-manually/getting-started-pleasanter-almalinux.md)
[プリザンターをRed Hat Enterprise Linux 8にインストールする](../../setup/installation/install-manually/getting-started-pleasanter-rhel-8.md)
[プリザンターをRed Hat Enterprise Linux 9.7/10.1にインストールする](../../setup/installation/install-manually/getting-started-pleasanter-rhel.md)

### Dockerで起動する

[Dockerイメージを使用しDBにMySQLを指定して起動する](../../setup/installation/running-with-docker/setup-by-docker-image-and-mysql.md)

### GitHubリポジトリのソースファイルで起動する

[GitHubリポジトリのソースコードおよびDockerで起動する](../../setup/installation/running-from-source/setup-by-github-sources-on-docker.md)

### 関連ソフトウェアのインストール

[MySQLのインストール（Windows OS）](../../setup/installation/install-database/install-mysql-on-windows.md)

### 移行

[異なる種類のDBにプリザンターのデータを移行する手順](../../setup/version-up-migration/migration/migrate.md)（バージョン1.4.13.0以降で対応）

### パラメータ設定

-   [パラメータ設定：Migration.json](../../setup/parameters/migration-json.md)
-   [パラメータ設定：Rds.json](../../setup/parameters/rds-json.md)

### 追加設定

-   [WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](../../setup/additional/db-server/mysql-create-user-by-sql.md)（バージョン1.4.10.0以降で対応）
-   [WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](../../setup/additional/db-server/mysql-connecting-host-description.md)（バージョン1.4.18.0以降で対応）

### FAQ：動作環境、セットアップ

[MySQLに関連するマニュアルを確認したい](faq-mysql-manual-list.md)
-   [FAQ：MySQLでWebサーバとDBサーバを分離した構成にしたい](faq-mysql-multiple-server.md)（バージョン1.4.10.0以降で対応）
-   [FAQ：プリザンターの動作環境や推奨スペックが知りたい](faq-recommended-specifications.md)
-   [FAQ：プリザンターの項目数が足りない場合(項目数を26個より多く増やしたい)](faq-missing-columns.md)

### FAQ：バックアップ、リストア

[FAQ：MySQL データベース バックアップ・リストア手順](../backup-restore/faq-mysql-backup-restore.md)（バージョン1.4.10.0以降で一部の手順を修正）

## 対応バージョン

| 対応バージョン | 内容                                                                                                        |
| :------------- | :---------------------------------------------------------------------------------------------------------- |
| 1.4.9.0 以降   | MySQLへの対応に伴いFAQを新規作成                                                                            |
| 1.4.9.2 以降   | MySQL環境でプリザンターセットアップ後の初回ログイン時、アプリケーションエラーが発生する場合がある問題を解消 |
| 1.4.10.0 以降  | MySQLのアクセス制御機能によりOwner、Userの接続が拒否される場合がある問題を解消                              |
| 1.4.13.0 以降  | プリザンターのDBをSQL ServerからMySQLに移行する機能を追加                                                   |
| 1.4.18.0 以降  | MySQLのDBへの接続元ホストにlocalhost（DBと同一のサーバ）以外を指定する機能を追加                            |
