---
title: プリザンターのリマインダー機能を有効化する（外部スクリプト）
category: 追加設定：通知
order: '210'
status: ''
parts: ''
urlstring: reminder-script
translationKey: reminder-script
shortname: リマインダー
created: 2025-03-07
updated: 2025-03-13
---

## 概要

[リマインダー](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)機能を有効化する方法を説明します。ご利用環境が以下に当てはまる場合に本手順でリマインダー機能を有効化してください。  

-   ご利用のプリザンターのバージョンが1.3.6以前である  
-   [統合Windows認証](../authn-authz/active-directory-sso.md)を有効とした環境である（バージョン問わず）

## 制限事項

1. プリザンターのバージョン 1.3.7.0 以降、リマインダーを有効化する手順が変更になりました。最新バージョンをご利用の場合は「プリザンターのリマインダー機能を有効化する」を確認してください。
1. 本手順の設定をしたまま、「プリザンターのリマインダー機能を有効化する」の手順で設定するとリマインダーが二重起動し、メールが複数回送信される可能性があります。

## 操作手順

リマインダーを動作させるスクリプトをタスクスケジューラまたはcronに登録します。

### Windowsでの設定方法

1. スクリプトの設置
    [Reminder.ps1](https://github.com/Implem/Implem.Pleasanter/blob/master/Implem.Pleasanter/Tools/Reminder.ps1)をD:\Tools等任意のフォルダにコピーします。Reminder.ps1をメモ帳等で編集しhttp://localhost/pleasanter/ の部分を、クライアントからアクセス可能なプリザンターのURLに変更します。例えばhttp://localhostとした場合でもリマインダーを動かす事ができますが、送信されたメールに記載されるレコードのURLがhttp://localhost/ となるため、レコードのリンクをクリックしてもクライアントからアクセスできません。  
    ※Azureで環境構築している場合はApp ServiceのWebジョブ登録にてReminder.ps1を使用することになりますが、その際は1行目のコメントアウトされた処理を有効化してください。

2. タスクスケジューラの設定
    スクリプトをタスクスケジューラに登録します。タスクの作成画面で下記の設定を行ってください。タスクを作成したら、タスクを右クリックして実行してください。  

|項目|設定内容|説明|
|:--|:--|:--|
|タスク名|Reminder|任意の名称を入力します。|
|ユーザがログオンしているかどうかにかかわらず実行する|有効|ログオフした状態でも動作します。|
|トリガー|スタートアップ時|サーバの起動時に開始します。|
|実行プログラム|%SystemRoot%\System32\  WindowsPowerShell\v1.0\  powershell.exe|PowerShellを実行します。|
|引数の追加|-ExecutionPolicy Bypass -Command ".\Reminder.ps1"|PowerShellから呼び出すスクリプトです。|
|開始|D:\Tools|Reminder.ps1を配置したディレクトリです。|
|タスクを停止するまでの時間|無効化|常駐プログラムとして動作し続けます。|

### Linuxでの設定方法

1. /web/pleasanter/Tools/Reminder.py を開いて localhost の部分を書き換え、クライアントからアクセス可能なURLに変更します。

    ```python
    urllib.request.Request("http://192.168.11.100/reminderschedules/remind?NoLog=1")
    ```

2. リマインダーを動作させるために必要な「Python3.6」をインストールします。

    ```bash
    sudo dnf install -y python36
    ```

3. Reminder.py を cron設定します。

    ```bash
    crontab -e
    @reboot python3 /web/pleasanter/Tools/Reminder.py
    ```

## 関連情報

-   [応用編：通知、リマインダー](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)
-   [統合Windows認証によるシングルサインオンを利用する](../authn-authz/active-directory-sso.md)
-   [Reminder.ps1](https://github.com/Implem/Implem.Pleasanter/blob/master/Implem.Pleasanter/Tools/Reminder.ps1)
