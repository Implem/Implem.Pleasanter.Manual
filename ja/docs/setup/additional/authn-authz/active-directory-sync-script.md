---
title: プリザンターにActive Directoryのユーザ情報を同期する（外部スクリプト）
category: 追加設定：認証
order: '210'
status: ''
parts: ''
urlstring: active-directory-sync-script
translationKey: active-directory-sync-script
shortname: LDAP同期
created: 2025-03-12
updated: 2025-03-13
---

## 概要

ActiveDirectoryなどのLDAPサーバとの同期処理を自動実行する方法を説明します。ご利用環境が以下に当てはまる場合に本手順で「[LDAP同期](active-directory-sync.md)」機能の定期実行を設定してください。  

-   ご利用のプリザンターのバージョンが1.3.18以前である  
-   [統合Windows認証](active-directory-sso.md)を有効とした環境である（バージョン問わず）

## 制限事項

1. プリザンターのバージョン1.3.19以降、LDAP同期処理を自動実行する手順が変更になりました。最新バージョンをご利用の場合は「プリザンターにActive Directoryのユーザ情報を同期する」を確認してください。
2. 本手順の設定をしたまま、「プリザンターにActive Directoryのユーザ情報を同期する」の手順で設定するとLDAP同期処理が二重起動し、設定内容によってはログインできなくなる可能性があります。

## 操作手順

LDAP同期処理を実行させるスクリプトをタスクスケジューラに登録します。

### 1. LDAP連携の設定

以下マニュアルページを参照しを[LDAP連携](active-directory.md)の設定を行います。
- [プリザンターとActive Directoryを連携する](active-directory.md)

### 2. LDAP同期処理の実行

下記のURLにリクエストを要求（ブラウザでURL実行、PowerShellのInvoke-RestMethodコマンド等）することでLDAP同期処理を実行します。{ServerName}は実行環境に合わせて変更してください。  
```
http(s)://{ServerName}/users/syncbyldap
```

### 3. 定期的に同期するための設定

タスクスケジューラを使用し定期的にActive Directoryの情報を同期する設定を行うことで、最新の人事データをプリザンターに取り込むことができます。

1. スクリプトの設置
下記のファイルの内容をD:\Tools等任意のフォルダにコピーします。
https://github.com/Implem/Implem.Pleasanter/blob/master/Implem.Pleasanter/Tools/SyncByLdap.ps1

2. タスクスケジューラの設定
タスクの作成画面で下記の設定を行ってください。タスクを作成したら、タスクを右クリックして実行してください。

|項目|設定内容|説明|
|:--|:--|:--|
|タスク名|SyncByLdap|任意の名称を入力します。|
|ユーザがログオンしているかどうかにかかわらず実行する|有効|ログオフした状態でも動作します。|
|トリガー|任意の周期|定期的にスクリプトを起動します。|
|実行プログラム|%SystemRoot%\System32\  WindowsPowerShell\v1.0\  powershell.exe|PowerShellを実行します。|
|引数の追加|-ExecutionPolicy Bypass -Command ".\SyncByLdap.ps1"|PowerShellから呼び出すスクリプトです。|
|開始|D:\Tools|SyncByLdap.ps1を配置したディレクトリです。|

## 関連情報

-   [統合Windows認証によるシングルサインオンを利用する](active-directory-sso.md)
-   [プリザンターとActive Directoryを連携する ― AD連携](active-directory.md)
