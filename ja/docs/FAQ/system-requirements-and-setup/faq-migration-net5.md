---
title: 以前のバージョンからプリザンター1.2以降への移行についてのよくある質問集
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-migration-net5
translationKey: faq-migration-net5
shortname: プリザンター12への移行
created: 2021-07-19
updated: 2023-11-09
---

[追記：2022/03/01【重要】プリザンター1.3よりターゲットフレームワークが.NET6に変更されます。](https://pleasanter.org/blogs/news-migrate-to-dotnet6)

## 概要

.NET Framework版、.NET Core版は統合されプリザンター1.2となりました。新たにリリースされたプリザンター1.2への移行についてのよくある質問のまとめです。

[プリザンター .NET Framework版と.NET Core版の統合について ](https://pleasanter.org/archives/net5_integration)

## 質問一覧

1. プリザンター Community Editionは引き続き無償で使えますか？
1. プリザンター1.2に移行しても既存のアプリ・データは引き続き使えますか？
1. プリザンター1.2はどういうものですか？
1. プリザンター1.2へ移行するには、WindowsからLinuxに移行する必要がありますか？
1. プリザンター1.2へ移行するには、SQL ServerからPostgreSQLに移行する必要がありますか？
1. プリザンター1.2へ移行するには、新しいOS環境を用意する必要がありますか？
1. .NET Framework版からの移行手順について教えてください。
1. .NET Core版からの移行手順について教えてください。
1. 2021年7月以降もプリザンター .NET Core版の提供は継続されますか？
1. プリザンター1.2への移行の支援はうけられますか？
1. プリザンター .NET Framework版の提供は継続されますか？
1. 2022年以降もプリザンター .NET Framework版のサポートは受けられますか？

## 質問と回答

### プリザンター Community Editionは引き続き無償で使えますか？

はい。プリザンター1.2も引き続き無償でご利用いただけます。Enterprise Editionをご利用いただけるサポートサービスを含め、その他有償サービスにつきましても、従来どおりのプランで提供いたします。

### プリザンター1.2に移行しても既存のアプリ・データは引き続き使えますか？

はい。移行後もアプリ・データに影響はありませんので、そのままお使いいただけます。

### プリザンター1.2は、どういうものですか？

.NET Core版のソースコードをベースに、ターゲットフレームワークを.NET Core3.1から.NET 5に変更したものです。Windows、Linux、UbuntuなどのOS環境と、SQL ServerまたはPostgreSQLのデータベースを組み合わせてご使用いただけます。

### プリザンター1.2へ移行するには、WindowsからLinuxに移行する必要がありますか？

いいえ、Windowsのままでお使いいただけます。

### プリザンター1.2へ移行するには、SQL ServerからPostgreSQLに移行する必要がありますか？

いいえ、SQL Serverのままでお使いいただけます。

### プリザンター1.2へ移行するには、新しいOS環境を用意する必要がありますか？

いいえ、今お使いのOS環境内でバージョンアップを行いそのままお使いいただけます。データ移行も必要ありません。

### .NET Framework版からの移行手順について教えてください。

[Windows/Windows Serverにインストールしたプリザンター 1.4をプリザンター 1.5へ移行する手順](../../setup/version-up-migration/migration/migrate-to-pleasanter-windows.md)<br>

### .NET Core版からの移行手順について教えてください。

[Ubuntuにインストールしたプリザンター 1.4をプリザンター 1.5へ移行する手順](../../setup/version-up-migration/migration/migrate-to-pleasanter-ubuntu.md)
[CentOSに構築した以前のプリザンター(.NET Core版)からプリザンター 1.3以降への移行手順](../../setup/version-up-migration/migration/migrate-to-pleasanter-centos.md)

### 2021年7月以降もプリザンター .NET Core版の提供は継続されますか？

プリザンター1.2は.NET Core版のターゲットフレームワークを変更したものです。.NET Core版は今後プリザンター1.2として継続して提供されます。

### プリザンター1.2への移行の支援はうけられますか？

はい、ご支援可能です。詳細はお問い合わせください。

### プリザンター .NET Framework版の提供は継続されますか？

.NET Framework版は、2021年12月まで最新バージョンが提供されます。2022年1月以降は、年間サポートサービスをご契約のユーザ様限定で不具合解消版が提供されます(新機能は含まれません)。

### 2022年以降もプリザンター .NET Framework版のサポートは受けられますか？

2022年以降もプリザンター .NET Framework版の年間サポートサービスは、新規契約、並びに継続が可能です。.NET Framework版のサポートサービスはリリース日から最長5年間提供されます。

## 関連情報

[CentOSに構築した以前のプリザンター(.NET Core版)からプリザンター 1.3以降への移行手順](../../setup/version-up-migration/migration/migrate-to-pleasanter-centos.md)  
[Ubuntuにインストールしたプリザンター 1.4をプリザンター 1.5へ移行する手順](../../setup/version-up-migration/migration/migrate-to-pleasanter-ubuntu.md)  
[Windows/Windows Serverにインストールしたプリザンター 1.4をプリザンター 1.5へ移行する手順](../../setup/version-up-migration/migration/migrate-to-pleasanter-windows.md)  
[プリザンターをWindows Server 2019にインストールする](../../setup/installation/install-manually/getting-started-pleasanter-windows-server2019.md)  
[プリザンターをWindows Server 2016にインストールする](../../setup/installation/install-manually/getting-started-pleasanter-windows-server2016.md)  
[プリザンターをWindows 11にインストールする](../../setup/installation/install-manually/getting-started-pleasanter-windows10.md)  
