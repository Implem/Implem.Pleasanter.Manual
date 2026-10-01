---
title: 環境別の自動再起動設定
category: パラメータ管理機能
order: '400'
status: ''
parts: ''
urlstring: manage-parameters-auto-reboot-settings
translationKey: manage-parameters-auto-reboot-settings
shortname: パラメータ管理機能：環境別の自動再起動設定
created: 2026-05-29
updated: 2026-06-09
---

## 概要

「再起動」ボタンによる再起動は、単にプリザンタープロセスの停止を意味します。そこで、起動プロセス管理を設定することで、プロセスの停止後に自動的に再起動するように設定します。

主な環境での設定方法は以下の通りです。

##### 各環境の比較表

|No| インフラ          | 自動再起動              | 追加設定                                          |
|---| ----------------- | ----------------------- | ------------------------------------------------- |
|1| Windows           | NSSMが自動再起動        | NSSMのインストールとサービス登録が必要            |
|2| Linux             | systemdが自動再起動     | サービスユニットファイルの作成が必要              |
|3| Azure App Service | App Serviceが自動再起動 | 「Always On」の有効化を推奨<br>（追加設定は基本不要） |
|4| Docker            | Dockerが自動再起動      | restart: unless-stoppedの設定が必要               |
|－| dotnet直接起動    | 自動再起動しない        | 手動での再起動が必要                              |

## 前提条件

1. 事前に下記マニュアルの手順を実施している必要があります。
   1. [パラメータ管理機能](index.md)
   1. [パラメータ管理機能：画面からの再起動](manage-parameters-reboot-from-screen.md)

## 1. Windows

Windows標準のサービスマネージャ（srvany）は、アプリケーションの強制終了やクラッシュ時にサービスが停止したままとなります。そこで、サードパーティ製のNSSM（Non-Sucking Service Manager）にプリザンターを登録し、プロセスが終了するとNSSMが自動的にプリザンターを再起動するように設定します。

#### 設定手順

1. PowerShellで以下のコマンドを実行し、NSSMをインストールしてください。

       ```ps1
       winget install NSSM.NSSM --source winget --silent --accept-source-agreements --accept-package-agreements
       ```

1. PowerShellで以下のコマンドを実行し、プリザンターをサービスとして登録してください。以下ではサービス名をPleasanterとしています。

       ```ps1
       nssm install Pleasanter "C:\Program Files\dotnet\dotnet.exe" "bin\Debug\net10.0\Implem.Pleasanter.dll --urls http://0.0.0.0:5000"
       nssm set Pleasanter AppDirectory "C:\web\pleasanter\Implem.Pleasanter"
       nssm set Pleasanter AppExit Default Restart
       nssm set Pleasanter AppRestartDelay 3000
       ```

       | 引数                    | 値                                               | 説明                           |
       | ----------------------- | ------------------------------------------------ | ------------------------------ |
       | AppDirectory            | "C:\web\pleasanter\Implem.Pleasanter" | アプリケーションルートを指定   |
       | AppExit Default Restart | Default Restart                                  | プロセス終了時に自動再起動する |
       | AppRestartDelay         | 3000                                             | 再起動までの待機時間（ミリ秒） |

1. PowerShellで以下のコマンドを実行し、NSSM経由でプリザンターのサービスを起動してください。

       ```ps1
       nssm start Pleasanter
       ```

#### サービス状態の確認

サービスの状態を確認するには、sc.exe（Windows Service Control Manager）を使います。query {サービス名}というサブコマンドを渡すと、サービスの現在の状態（実行中・停止など）を表示します。PowerShellで以下のコマンドを実行してください。

```ps1
sc.exe query Pleasanter
```

## 2. Linux

以下の各ページで作成したPleasanterサービス用スクリプト「pleasanter.service」を使用します。

-   [インストーラでプリザンターをUbuntuにインストールする](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-ubuntu.md)  
-   [インストーラでプリザンターをAlmaLinuxにインストールする](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)  
-   [インストーラでプリザンターをRed Hat Enterprise Linux 9.7/10.1にインストールする](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-rhel9.md)  
-   [インストーラでプリザンターをRed Hat Enterprise Linux 8にインストールする](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-rhel-8.md)  

※pleasanter.serviceの内容は、プラットフォームを問わず共通です。

#### 設定手順

1. 上記インストールの手順で作成したpleasanter.serviceの「Restart」と「RestartSec」に、それぞれ下表の値が設定されていることを確認してください。

       | 設定       | 値     | 説明                               |
       | ---------- | ------ | ---------------------------------- |
       | Restart    | always | プロセス終了時に常に自動再起動する |
       | RestartSec | 10     | 再起動までの待機時間（秒）         |

       ##### pleasanter.service（10～11行目）
       ```ini
       Restart = always
       RestartSec = 10
       ```

1. 以下のコマンドを実行してください。作成したPleasanterサービス用スクリプトをsystemdに認識させ、サーバが起動した際にプリザンターサービスが起動するように設定したうえで、プリザンターを即時起動します。

       ```bash
       sudo systemctl daemon-reload
       sudo systemctl enable pleasanter
       sudo systemctl start pleasanter
       ```

#### サービス状態・再起動回数の確認

サービスの状態を確認するには、systemctlコマンドを使います。show {サービス名}でサービスの情報を表示します。ActiveStateプロパティは稼働中か否か（active/inactive）を、SubStateプロパティは稼働中であればrunning（正常稼働中）であることを表します。

以下は、自動再起動の回数を含めて確認するコマンドです。

```bash
systemctl show pleasanter.service --property=NRestarts,ActiveState,SubState
```

## 3. Azure App Service

Azure App Serviceはデフォルトでプロセスの自動再起動をサポートしています。マニュアル通りにセットアップしていれば、追加設定は不要ですが、以下を確認してください。

#### 設定手順

1. [Azure Portal](https://portal.azure.com/)に接続し、App Serviceを開いてください。
1. 「構成」メニューの「全般設定」を開いて、「Always On」を有効化してください。

       ![Azure PortalのApp Serviceの「構成」－「全般設定」画面。「Always On」がある](https://pleasanter.org/files/images/ja/managers-guide/manage-parameter/assets/567eea88796049baa1d4c2b9aa03068d.png)

App Serviceはプロセスの終了を検知すると、自動的に再起動します。再起動は数秒以内に完了します。追加の起動プロセス管理設定は不要です。

## 4. Docker

Dockerに再起動ポリシー「restart: unless-stopped」を設定し、コンテナが終了した際に自動的に再起動するように設定してください。

#### 主な再起動ポリシー

| ポリシー       | 説明                             |
| -------------- | -------------------------------- |
| no             | 再起動しない（デフォルト）       |
| always         | 常に再起動する                   |
| unless-stopped | 手動停止以外は再起動する（推奨） |
| on-failure     | 異常終了時のみ再起動する         |

#### 設定手順

「[Dockerで起動する](../../setup/installation/running-with-docker/getting-started-pleasanter-docker.md)」で作成したdocker-compose.ymlを下記のとおり編集してください。

##### 編集前のdocker-compose.yml（15～18行目）

```yaml
  pleasanter:
    container_name: pleasanter
    image: implem/pleasanter:${PLEASANTER_VERSION}
    depends_on:
      : 後略
```

##### 編集後のdocker-compose.yml（15～19行目）

```yaml
  pleasanter:
    container_name: pleasanter
    image: implem/pleasanter:${PLEASANTER_VERSION}
    restart: unless-stopped  # ←この行を追加
    depends_on:
      : 後略
```

#### コンテナの状態・再起動回数の確認

サービスの状態を確認するには、inspectコマンドを使います。--formatオプションの引数に{.RestartCount}と{.State.Status}を渡すことで、再起動回数やコンテナの状態を確認できます。

```ps1
docker inspect <コンテナ名> --format '{{.RestartCount}} {{.State.Status}}'
```

## 関連情報

-   [パラメータ管理機能](index.md)
-   [パラメータ管理機能：画面からの再起動](manage-parameters-reboot-from-screen.md)
-   [Azure Portal](https://portal.azure.com/)
