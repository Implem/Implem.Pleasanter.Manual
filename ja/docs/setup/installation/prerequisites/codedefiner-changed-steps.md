---
title: ver1.4.6以降で初回インストール時のCodeDefinerの手順について
category: インストール時の注意事項
order: '200'
status: ''
parts: ''
urlstring: codedefiner-changed-steps
translationKey: codedefiner-changed-steps
shortname: ''
created: 2024-07-16
updated: 2026-01-13
---

## 概要

ver1.4.6以降、初回インストール時のCodeDefinerのコマンドが変更となりました。
<span class="pl-attention">バージョンアップ時の手順に変更はありません。</span>

 ---

## Azure

##### ver.1.4.5まで

```
dotnet Implem.CodeDefiner.dll _rds /p C:\home\site\wwwroot
```

##### ver.1.4.6以降

※下記コマンドは初回インストール時にのみ実行します。

```
dotnet Implem.CodeDefiner.dll _rds /p C:\home\site\wwwroot /l "ja" /z "Tokyo Standard Time"
```

## Windows

##### ver.1.4.5まで

```
dotnet Implem.CodeDefiner.dll _rds
```

##### ver.1.4.6以降

※下記コマンドは初回インストール時にのみ実行します。

```
dotnet Implem.CodeDefiner.dll _rds /l "ja" /z "Tokyo Standard Time"
```

## Linux

##### ver.1.4.5まで

```
sudo -u <プリザンターを起動するユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds
```

##### ver.1.4.6以降

※下記コマンドは初回インストール時にのみ実行します。

```
sudo -u <プリザンターを起動するユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds /l "ja" /z "Asia/Tokyo"
```

## Docker

##### ver.1.4.5まで

```
docker compose run --rm codedefiner _rds
```

##### ver.1.4.6以降

※下記コマンドは初回インストール時にのみ実行します。

```
docker compose run --rm codedefiner _rds /l "ja" /z "Asia/Tokyo"
```

### 各環境のインストール手順は以下を参照してください。

[プリザンターをAzure App Serviceにサーバレス構成でインストールする](../install-manually/getting-started-pleasanter-azure.md)
[プリザンターをWindowsにインストールする](../install-manually/getting-started-pleasanter-windows.md)
[プリザンターをUbuntuにインストールする](../install-manually/getting-started-pleasanter-ubuntu.md)
[プリザンターをAlmaLinuxにインストールする](../install-manually/getting-started-pleasanter-almalinux.md)
[プリザンターをRed Hat Enterprise Linux 8にインストールする](../install-manually/getting-started-pleasanter-rhel-8.md)
[プリザンターをRed Hat Enterprise Linux 9.7/10.1にインストールする](../install-manually/getting-started-pleasanter-rhel.md)
[Dockerで起動する](../running-with-docker/getting-started-pleasanter-docker.md)
