---
title: .NET 8のインストール（Windows環境）
category: .NETのインストール
order: '200'
status: ''
parts: ''
urlstring: install-dotnet-8-windows
translationKey: install-dotnet-8-windows
shortname: ''
created: 2025-12-23
updated: 2026-01-13
---

## 概要

.NET 8のインストール手順です。Windows環境でプリザンターをセットアップする前に必ず実施してください。

## 前提条件

1. プリザンター1.5.0.0以降を利用する場合は、[.NET 10.0.xをインストール](install-dotnet-windows.md)してください。
1. Hosting Bundleをインストールしないとプリザンターが起動しません。手順を確認の上、.NETとHosting Bundleそれぞれのインストールを行ってください。

## .NET 8.0のインストール

.NET 8.0の「SDK 8.0.x」と「Hosting Bundle」の2つをインストールしてください。

## 手順

.NETのインストール手順は以下の通りです。

1.  SDKのインストール
1.  Hosting Bundleのインストール

## SDKのインストール

1.  ブラウザを起動し、以下のURLへアクセスしてください。

    [https://dotnet.microsoft.com/download/dotnet/8.0](https://dotnet.microsoft.com/download/dotnet/8.0)

1.  「SDK 8.0.x」をダウンロードし、インストールしてください。

    ![.NET 8.0 のダウンロードページ。「SDK 8.0.x」のダウンロードリンクがある](https://pleasanter.org/files/images/ja/setup/installation/install-dotnet/assets/31c43c2944e547c88b8f0620231a12f3.png)

1. コマンドプロンプトまたはPowerShellを起動して以下のコマンドを実行し、「8.0.x」が表示されることを確認してください。

    ``` ps1
    dotnet --version
    ```

## Hosting Bundleのインストール

1. 「Hosting Bundle」をダウンロードし、インストールしてください。

    ![.NET 8.0 のダウンロードページ。「Hosting Bundle」のダウンロードリンクがある](https://pleasanter.org/files/images/ja/setup/installation/install-dotnet/assets/deba23e6b5474821b6d4ac4e2d0d6b34.png)

## 関連情報

-   [.NET 10のインストール（Windows環境）](install-dotnet-windows.md)
-   [FAQ：プリザンターインストール後、ログイン画面にアクセスするとHTTP500エラーが発生し、ログイン画面が表示されない](../../../FAQ/system-requirements-and-setup/faq-httperror-after-installation.md)
