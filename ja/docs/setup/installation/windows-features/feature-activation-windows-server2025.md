---
title: Windowsの機能の有効化（Windows Server 2025）
category: Windowsの機能の有効化
order: '100'
status: ''
parts: ''
urlstring: feature-activation-windows-server2025
translationKey: feature-activation-windows-server2025
shortname: Windows Server 2025の機能の有効化
created: 2025-11-13
updated: 2026-01-13
---

## Windowsの機能の有効化

1. 「サーバー マネージャー」を起動してください。
1. 「管理」メニューを開き「役割と機能の追加」をクリックしてください。  
![サーバー マネージャーの「管理」メニュー。「役割と機能の追加」がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/44809b816b674818944a17bdc7b32459.png)
1. 「開始する前に」画面が表示されるので「次へ」ボタンをクリックしてください。  
![「役割と機能の追加ウィザード」の「開始する前に」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/4ac476044b7247dca0328061609dd6bd.png)
1. 「インストールの種類の選択」画面が表示されるので「次へ」ボタンをクリックしてください。  
![「インストールの種類の選択」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/b22fb81e8c174d04b711880ee27ae8f4.png)
1. 「対象サーバーの選択」画面が表示されるので対象サーバーを選択し「次へ」ボタンをクリックしてください。  
![「対象サーバーの選択」画面。対象サーバーの一覧がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/aad8c2c9ac014ea2b05c864fdbbec597.png)
1. 「サーバーの役割の選択」画面が表示されるので「Web サーバー (IIS)」にチェックを入れてください。  
![「サーバーの役割の選択」画面。「Web サーバー (IIS)」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/a075c3e7fc284b7aa7bf3b688e9e16c5.png)
1. 「Web サーバー (IIS) に必要な機能を追加しますか？」画面が表示されるので「管理ツールを含める (存在する場合)」にチェックを付け、「機能の追加」ボタンをクリックしてください。  
![「Web サーバー (IIS) に必要な機能を追加しますか？」画面。「機能の追加」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/3946123263144b9db2a5c6616ee6f21d.png)
1. 「Web サーバー (IIS)」にチェックが入ったことを確認し「次へ」ボタンをクリックしてください。  
![「サーバーの役割の選択」画面。「Web サーバー (IIS)」にチェックが入った状態](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/7b92d577d2924beaa9ba8782f384ab50.png)
1. 「機能の選択」画面が表示されるので「次へ」ボタンをクリックしてください。  
![「機能の選択」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/95f822b82f054dca9511b4135163f8d9.png)
1. 「Web サーバーの役割 (IIS)」画面が表示されるので「次へ」ボタンをクリックしてください。  
![「Web サーバーの役割 (IIS)」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/5149477b9d3048bca54e19d4b3c0f33c.png)
1. 「役割サービスの選択」画面が表示されるので「次へ」ボタンをクリックしてください。  
![「役割サービスの選択」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/08474ed493ef466799442495142f172d.png)
1. 「インストール オプションの確認」画面が表示されるので「インストール」ボタンをクリックしてください。  
![「インストール オプションの確認」画面。「インストール」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/eb7f884fca324a2cbfcb290accbfa3cd.png)
1.  インストールの完了を待ちます。  
![インストールを実行している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/132ed6f14675475681c207f6e39b7de2.png)
1. インストールの完了後、「閉じる」ボタンをクリックしてください。
![インストールの完了画面。「閉じる」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/662a7b35aa374fda9a4df912e3934fa1.png)

## IISの設定変更

1. 「サーバー マネージャー」の「ツール」メニューを開き「インターネット インフォメーション サービス (IIS) マネージャー」を起動してください。
![サーバー マネージャーの「ツール」メニュー。IIS マネージャーの項目がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/ceb9f9cf91ba416ba03bd4986823d3c9.png)
1. 「アプリケーション プール」の「DefaultAppPool」を選択し、「アプリケーション プール既定値の設定」をクリックしてください。
![IIS マネージャーの「アプリケーション プール」画面。「アプリケーション プール既定値の設定」がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/32d3427646c7467797d6ded3d00dc31b.png)
1. 「プロセス モデル」の「アイドル タイムアウトの操作」を、「Terminate」から「Suspend」に変更し、「OK」をクリックしてください。
![「アプリケーション プール既定値」ダイアログ。「アイドル タイムアウトの操作」を「Suspend」に変更する](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/975ece572f76445f9f4b6d76116205d7.png)