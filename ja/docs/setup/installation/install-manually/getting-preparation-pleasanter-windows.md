---
title: プリザンターをWindowsにインストールする際の事前準備
category: プリザンターのインストール
order: '100'
status: ''
parts: ''
urlstring: getting-preparation-pleasanter-windows
translationKey: getting-preparation-pleasanter-windows
shortname: ''
created: 2025-03-14
updated: 2026-01-13
---

## 概要

プリザンターをWindows ServerまたはWindowsにインストールする際の事前準備です。  

## 前提となるソフトウェアのインストールおよび設定

プリザンターをインストールするためには、下記のソフトウェアのインストールおよび設定が必要になります。以下の手順通り、すべてインストールしてください。

### 1. Windowsの機能の有効化

インストールするOSに合わせていずれかの作業を実施してください。  

[Windowsの機能の有効化（Windows Server 2025）](../windows-features/feature-activation-windows-server2025.md)
[Windowsの機能の有効化（Windows Server 2022）](../windows-features/feature-activation-windows-server2022.md)
[Windowsの機能の有効化（Windows Server 2019）](../windows-features/feature-activation-windows-server2019.md)
[Windowsの機能の有効化（Windows Server 2016）](../windows-features/feature-activation-windows-server2016.md)
[Windowsの機能の有効化（Windows 11）](../windows-features/feature-activation-windows10.md)

### 2. .NETのインストール

プリザンター1.5系をインストールする場合は、.NET 10をインストールしてください。  
プリザンター1.4系をインストールする場合は、.NET 8をインストールしてください。

[.NET 10のインストール（Windows環境）](../install-dotnet/install-dotnet-windows.md)
[.NET 8のインストール（Windows環境）](../install-dotnet/install-dotnet-8-windows.md)

### 3. データベースのインストール

#### DBにSQL Serverを利用する場合

SQL Server Expressは2025と2022でデータベースの最大容量に差があります。詳細は「[FAQ：SQL Server Expressの制約について教えてください。](../../../FAQ/system-requirements-and-setup/faq-sql-server-express-restriction.md)」を参照してください。

[SQL Server 2025 Expressのインストールおよび設定](../install-database/install-sql-server2025-express.md)
[SQL Server 2022 Expressのインストールおよび設定](../install-database/install-sql-server2022-express.md)
[SQL Server Management Studioのインストール](../install-database/install-sql-server-management-studio.md)

#### DBにPostgreSQLを利用する場合

[PostgreSQL 18のインストール（Windows OS）](../install-database/install-postgresql-on-windows.md)
[PostgreSQL 17のインストール（Windows OS）](../install-database/install-postgresql17-on-windows.md)

#### DBにMySQLを利用する場合

[MySQLのインストール（Windows OS）](../install-database/install-mysql-on-windows.md)

※MySQLはver1.4.9.0以降で使用できます。ver1.4.9.0より前のプリザンターはMySQLに対応していません。

#### MySQLを利用かつWebサーバとDBサーバを分離する場合の追加手順

WebサーバとDBサーバを同一サーバ上で運用するは実施不要です。

[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](../../additional/db-server/mysql-connecting-host-description.md)  
[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](../../additional/db-server/mysql-create-user-by-sql.md)  

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.9.0 以降|MySQLに対応|
|1.4.10.0 以降|MySQLのアクセス制御機能によりOwner、Userの接続が拒否される場合がある問題を解消|
|1.4.18.0 以降|MySQLのDBへの接続元ホストにlocalhost（DBと同一のサーバ）以外を指定する機能を追加|
|1.5.0.0 以降|.NET 10、Windows Server 2025、SQL Server 2025、PostgreSQL 18に対応|