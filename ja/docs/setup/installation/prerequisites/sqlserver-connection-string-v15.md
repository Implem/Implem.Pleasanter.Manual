---
title: プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項
category: インストール時の注意事項
order: '100'
status: ''
parts: ''
urlstring: sqlserver-connection-string-v15
translationKey: sqlserver-connection-string-v15
shortname: プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項
created: 2026-01-09
updated: 2026-01-13
---

## 概要

プリザンター1.5以降で使用する.NET 10から、SQL Serverへの接続時にTLS証明書検証がデフォルトで有効化されました。

この変更により、接続先のSQL Serverが有効なTLS証明書を提示しない場合、接続に失敗する可能性があります。プリザンター1.4以前で使用する.NET 8は、TLS証明書検証がデフォルトで無効化されていたため、証明書未設定のSQL Serverに対して接続できましたが、プリザンター1.5以降では以下の対応が必要です。

### 対応方法

1. SQL ServerにTLS証明書を設定する
2. 接続文字列にTrustServerCertificate=true;を追加する

このページでは、TLS証明書の設定をすぐに行えないユーザ向けに、2.の方法を説明します。

## 操作手順

### 1.[Rds.json](../../parameters/rds-json.md)で設定している場合

##### 編集前のRds.json（該当部分のみ）

```json
    "SaConnectionString": "Server=(local);Database=master;UID=sa;PWD={※1};Connection Timeout=30;",
    "OwnerConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_Owner;PWD={※2};Connection Timeout=30;",
    "UserConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_User;PWD={※3};Connection Timeout=30;",
```

##### 編集後のRds.json（該当部分のみ）

```json
    "SaConnectionString": "Server=(local);Database=master;UID=sa;PWD={※1};Connection Timeout=30;TrustServerCertificate=true;",
    "OwnerConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_Owner;PWD={※2};Connection Timeout=30;TrustServerCertificate=true;",
    "UserConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_User;PWD={※3};Connection Timeout=30;TrustServerCertificate=true;",
```
{※1}　SAアカウントのパスワード  
{※2}、{※3}　任意のパスワード

### 2. システム環境変数で設定している場合

以下の各システム変数の値の末尾へ「TrustServerCertificate=true;」を追加してください。

1. Implem.Pleasanter_Rds_SQLServer_OwnerConnectionString
1. Implem.Pleasanter_Rds_SQLServer_SaConnectionString
1. Implem.Pleasanter_Rds_SQLServer_UserConnectionString

## TrustServerCertificate=true;を追記することの意味

接続文字列にTrustServerCertificate=true;を追記すると、クライアント側ではSQL Serverのサーバ証明書のチェーンを検証せずに（該当サーバ証明書を信頼して）、（暗号化以外の異常がある場合を除き）接続は必ず成功します。

サーバ証明書を導入していない場合、中間者攻撃などに対して無力になる可能性があり、使用は

1. ローカルサーバ
1. 開発用サーバ

など限定的な範囲に留めるべきとされています。

[マイクロソフト社のドキュメント](https://learn.microsoft.com/ja-jp/dotnet/framework/data/adonet/connection-string-syntax#use-trustservercertificate)を併せて確認してください。

## 関連情報

- [Rds.json](../../parameters/rds-json.md)
- [接続文字列の構文 - ADO.NET | Microsoft Learn - TrustServerCertificate の使用](https://learn.microsoft.com/ja-jp/dotnet/framework/data/adonet/connection-string-syntax#use-trustservercertificate)

### インストール

- [インストーラでプリザンターをWindowsにインストールする](../install-with-installer/getting-started-installer-pleasanter-windows.md)
- [プリザンターをWindowsにインストールする](../install-manually/getting-started-pleasanter-windows.md)
- [プリザンターをWindows Server 2025にインストールする](../install-manually/getting-started-pleasanter-windows-server2025.md)
- [プリザンターをWindows Server 2022にインストールする](../install-manually/getting-started-pleasanter-windows-server2022.md)
- [プリザンターをWindows Server 2019にインストールする](../install-manually/getting-started-pleasanter-windows-server2019.md)
- [プリザンターをWindows Server 2016にインストールする](../install-manually/getting-started-pleasanter-windows-server2016.md)
- [プリザンターをWindows 11にインストールする](../install-manually/getting-started-pleasanter-windows10.md)

### バージョンアップ

- [インストーラを利用したバージョンアップ手順(Windows)](../../version-up-migration/version-up-installer/version-up-installer-windows.md)
- [1.4.8.0以降のバージョンアップ手順(Windows)](../../version-up-migration/version-up-manually/version-up-windows-1.4.8.0.md)
- [プリザンターのバージョンアップ手順(Windows)](../../version-up-migration/version-up-manually/version-up-net.md)
- [Windows/Windows Serverにインストールしたプリザンター 1.4をプリザンター 1.5へ移行する手順](../../version-up-migration/migration/migrate-to-pleasanter-windows.md)