---
title: CodeDefinerを使ったトライアル開始
category: トライアル
order: '1200'
status: ''
parts: ''
urlstring: pleasanter-extensions-trial-codedefiner-start
translationKey: pleasanter-extensions-trial-codedefiner-start
shortname: CodeDefinerを使ったトライアル開始
created: 2025-12-01
updated: 2025-12-03
---

## 概要

CodeDefinerを使い、手動でPleasanter Extensionsのトライアルを開始する方法を説明します。

!!! tip "CodeDefinerのコマンド"
    CodeDefinerのコマンドについては[こちら](../../setup/codedefiner/codedefiner-command.md)を確認してください。

## 前提条件

-   以下の手順では、プリザンターがインストール済みであることを前提とします。以下の手順では、プリザンターはインストールされないことに注意してください。

## 操作手順

各パスは、本ユーザマニュアルの手順に従ってインストールした場合の一例です。利用中の環境に応じて、適宜読み替えてください。

=== ":fontawesome-brands-windows: Windowsの場合"

    1.  コマンドプロンプトまたはWindows PowerShellを開き、以下のコマンドを実行してください。

        ``` text title="trialオプション付きでCodeDefinerを実行"
        cd C:\web\pleasanter\Implem.CodeDefiner
        dotnet Implem.CodeDefiner.dll trial
        ```

    1.  トライアルを開始することを確認してください。++y++ と入力し、++enter++ キーを押下してください。

        ``` text title="トライアル開始の確認" hl_lines="3"
        <INFO> Configurator.OutputLicenseInfo: This Edition is "Community Edtion".
        Type "y" (yes) to continue the Pleasanter Extensions Trial process, otherwise type "n" (no).
        y
        ```

=== ":fontawesome-brands-linux: Linuxの場合"

    1.  以下のコマンドを実行します。`<プリザンター起動ユーザ>`には「Pleasanterサービス用スクリプト」で指定するユーザを指定します。

        ``` text title="trialオプション付きでCodeDefinerを実行"
        cd /web/pleasanter/Implem.CodeDefiner
        sudo -u <プリザンター起動ユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll trial
        ```

    1. トライアルを開始することを確認してください。++y++ と入力し、++enter++ キーを押下してください。

        ``` text title="トライアル開始の確認" hl_lines="3"
        <INFO> Configurator.OutputLicenseInfo: This Edition is "Community Edtion".
        Type "y" (yes) to continue the Pleasanter Extensions Trial process, otherwise type "n" (no).
        y
        ```

=== ":material-microsoft-azure: Azure App Serviceの場合"

    1.  Kuduのディレクトリ一覧からCodeDefinerを選択し、プロンプトが`C:\home\site\CodeDefiner`となることを確認します。
    1.  次のコマンドを実行します。

        ``` text title="trialオプション付きでCodeDefinerを実行"
        dotnet Implem.CodeDefiner.dll trial /p C:\home\site\wwwroot
        ```

    1. トライアルを開始することを確認してください。++y++ と入力し、++enter++ キーを押下してください。

        ``` text title="トライアル開始の確認" hl_lines="3"
        <INFO> Configurator.OutputLicenseInfo: This Edition is "Community Edtion".
        Type "y" (yes) to continue the Pleasanter Extensions Trial process, otherwise type "n" (no).
        y
        ```
