---
title: .NET 10のインストール（Windows環境）
category: .NETのインストール
order: '100'
status: ''
parts: ''
urlstring: install-dotnet-windows
translationKey: install-dotnet-windows
shortname: .NET
created: 2024-05-23
updated: 2026-01-13
---

## 概要

.NET 10のインストール手順です。Windows環境でプリザンターをセットアップする前に必ず実施してください。

## 前提条件

1.  プリザンター1.4系を利用する場合は、[.NET 8をインストール](install-dotnet-8-windows.md)してください。
1.  Hosting Bundleをインストールしないとプリザンターが起動しません。手順を確認の上、.NETとHosting Bundleそれぞれのインストールを行ってください。

## .NET 10.0のインストール

.NET 10.0の「SDK 10.0.x」と「Hosting Bundle」の2つをインストールしてください。

## 手順

.NETのインストール手順は以下の通りです。

1.  SDKのインストール
1.  Hosting Bundleのインストール

## SDKのインストール

1.  ブラウザを起動し、以下のURLへアクセスしてください。

    [https://dotnet.microsoft.com/download/dotnet/10.0](https://dotnet.microsoft.com/download/dotnet/10.0)

1.  「SDK 10.0.x」をダウンロードし、インストールしてください。

    ![.NET 10.0 のダウンロードページ。「SDK 10.0.x」のダウンロードリンクがある](https://pleasanter.org/files/images/ja/setup/installation/install-dotnet/assets/3908c21830a949b1a41220b880c362ec.png)

1.  コマンドプロンプトまたはPowerShellを起動して以下のコマンドを実行し、「10.0.x」が表示されることを確認してください。

    ``` ps1
    dotnet --version
    ```

## Hosting Bundleのインストール

1.  「Hosting Bundle」をダウンロードし、インストールしてください。

    ![.NET 10.0 のダウンロードページ。「Hosting Bundle」のダウンロードリンクがある](https://pleasanter.org/files/images/ja/setup/installation/install-dotnet/assets/d4b3ffde58e14e91bcd1c416f31b9db3.png)

## 関連情報

-   [.NET 8のインストール（Windows環境）](install-dotnet-8-windows.md)
-   [FAQ：プリザンターインストール後、ログイン画面にアクセスするとHTTP500エラーが発生し、ログイン画面が表示されない](../../../FAQ/system-requirements-and-setup/faq-httperror-after-installation.md)
