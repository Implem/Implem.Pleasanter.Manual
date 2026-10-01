---
title: Windowsの機能の有効化（Windows Server 2019）
category: Windowsの機能の有効化
order: '300'
status: ''
parts: ''
urlstring: feature-activation-windows-server2019
translationKey: feature-activation-windows-server2019
shortname: ''
created: 2019-06-16
updated: 2026-01-13
---

## Windowsの機能の有効化

1. 「サーバマネージャー」を起動してください。

1. 「管理(M)」メニューを開き「役割と機能の追加」をクリックしてください。  
![サーバマネージャーの「管理(M)」メニュー。「役割と機能の追加」がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/e5a81cbe97fe479398267775d31e1862.png)

1. 「開始する前に」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「役割と機能の追加ウィザード」の「開始する前に」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/9b8ae1f0cb914b1c929be4c14558cd49.png)

1. 「インストールの種類の選択」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「インストールの種類の選択」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/2c64088e4a044104bd7916c5c8afbb74.png)

1. 「サーバの選択」画面が表示されるので対象サーバを選択し「次へ(N)」ボタンをクリックしてください。  
![「サーバの選択」画面。対象サーバの一覧がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/c8393521964a48ccb7b51c38af90f24a.png)

1. 「サーバの役割の選択」画面が表示されるので「Webサーバ(IIS)」にチェックを入れてください。  
![「サーバの役割の選択」画面。「Webサーバ(IIS)」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/5f0266ac9b884df9b1ecb8fd64bf55b7.png)

1. 「Webサーバ(IIS)に必要な機能を追加しますか？」画面が表示されるので「管理ツールを含める(存在する場合)」にチェックを付け、「機能の追加」ボタンをクリックしてください。  
![「Webサーバ(IIS)に必要な機能を追加しますか？」画面。「機能の追加」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/ba640fd0301149f6a6325aab0e851051.png)

1. 「Webサーバ(IIS)」にチェックが入ったことを確認し「次へ(N)」ボタンをクリックしてください。  
![「サーバの役割の選択」画面。「Webサーバ(IIS)」にチェックが入った状態](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/ca4c79da44da436c951f75a77b6a1203.png)

1. 「機能」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「機能」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/6e998372de6d493489a017193d93dd53.png)

1. 「Webサーバの役割(IIS)」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「Webサーバの役割(IIS)」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/b3471179ae9c4c1ba23f03a122403c68.png)

1. 「役割サービスの選択」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「役割サービスの選択」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/4718137a9d4c43279b3e98d10344289e.png)

1. 「インストールオプションの確認」画面が表示されるので「インストール(I)」ボタンをクリックしてください。  
![「インストールオプションの確認」画面。「インストール(I)」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/ba88c2453bcc40e1beaa4bfb87485f63.png)

1.  インストールの完了を待ちます。  
![インストールを実行している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/0bf8b31b6687401aaeb28d163e68e5f0.png)

1. インストールの完了後、「閉じる」ボタンをクリックしてください。

## IISの設定変更

1. 「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS)マネージャー」を起動してください。
1. 「アプリケーションプール」の「DefaultAppPool」を選択し、「アプリケーションプール既定値の設定」をクリックしてください。
![IISマネージャーの「アプリケーションプール」画面。「アプリケーションプール既定値の設定」がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/f5ea5c36b6964f21b7159acde5123ede.png)
1. 「プロセスモデル」の「アイドルタイムアウトの操作」を、「Terminate」から「Suspend」に変更し、「OK」をクリックしてください。
![「アプリケーションプール既定値」ダイアログ。「アイドルタイムアウトの操作」を「Suspend」に変更する](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/9ab5568cacd14a568f5b73e1a238c9a7.png)