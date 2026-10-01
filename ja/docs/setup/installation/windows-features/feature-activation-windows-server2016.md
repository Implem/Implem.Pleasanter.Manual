---
title: Windowsの機能の有効化（Windows Server 2016）
category: Windowsの機能の有効化
order: '400'
status: ''
parts: ''
urlstring: feature-activation-windows-server2016
translationKey: feature-activation-windows-server2016
shortname: ''
created: 2019-04-28
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

1. 「機能の選択」画面が表示されるので「.NET Framework 3.5 Features」にチェックを入れ「次へ(N)」ボタンをクリックしてください。  
「指定されたサーバーで機能を追加または削除する要求に失敗しました。」というエラーが発生する場合、「.NET Framework 3.5 Features」のチェックを入れずに(未チェック)で進めると正常にインストールが継続できる場合があります。
![「機能の選択」画面。「.NET Framework 3.5 Features」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/ba41348a9da648199cc768bda66a6744.png)

1. 「Webサーバの役割(IIS)」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「Webサーバの役割(IIS)」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/b3471179ae9c4c1ba23f03a122403c68.png)

1. 「役割サービスの選択」画面が表示されるので「アプリケーション開発」配下の「ASP.NET 4.6」にチェックを入れてください。  
![「役割サービスの選択」画面。「アプリケーション開発」配下に「ASP.NET 4.6」がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/8447be927e1b4c4ba5018ee33d911ee4.png)

1. 「ASP.NET 4.6に必要な機能を追加しますか？」画面が表示されるので「機能の追加」ボタンをクリックしてください。  
![「ASP.NET 4.6に必要な機能を追加しますか？」画面。「機能の追加」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/d40a9a3a1d3c47b3a46abd20da9b647e.png)

1. 「ASP.NET 4.6」にチェックが入ったことを確認し「次へ(N)」ボタンをクリックしてください。  
![「役割サービスの選択」画面。「ASP.NET 4.6」にチェックが入った状態](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/00e7979764544d1fad99c1957f9da3f0.png)

1. 「インストールオプションの確認」画面が表示されるので「インストール(I)」ボタンをクリックしてください。  
![「インストールオプションの確認」画面。「インストール(I)」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/e869b7527fea40d488e96079271c5b3a.png)

1.  インストールの完了を待ちます。  
![インストールを実行している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/1d824efc74e841e99d59c58d01117212.png)

1. インストールの完了後、「閉じる」ボタンをクリックしてください。

## IISの設定変更

1. 「サーバマネージャー」から「インターネットサービス（IIS)マネージャー」を起動してください。
1. 「アプリケーションプール」の「DefaultAppPool」を選択し、「アプリケーションプール既定値の設定」をクリックしてください。
![IISマネージャーの「アプリケーションプール」画面。「アプリケーションプール既定値の設定」がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/f5ea5c36b6964f21b7159acde5123ede.png)
1. 「プロセスモデル」の「アイドルタイムアウトの操作」を、「Terminate」から「Suspend」に変更し、「OK」をクリックしてください。
![「アプリケーションプール既定値」ダイアログ。「アイドルタイムアウトの操作」を「Suspend」に変更する](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/9ab5568cacd14a568f5b73e1a238c9a7.png)