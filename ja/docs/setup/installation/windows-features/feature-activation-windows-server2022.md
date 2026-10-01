---
title: Windowsの機能の有効化（Windows Server 2022）
category: Windowsの機能の有効化
order: '200'
status: ''
parts: ''
urlstring: feature-activation-windows-server2022
translationKey: feature-activation-windows-server2022
shortname: ''
created: 2022-02-01
updated: 2026-01-13
---

## Windowsの機能の有効化

1. 「サーバマネージャー」を起動してください。

1. 「管理(M)」メニューを開き「役割と機能の追加」をクリックしてください。  
![サーバマネージャーの「管理(M)」メニュー。「役割と機能の追加」がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/e5a81cbe97fe479398267775d31e1862.png)
1. 「開始する前に」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「役割と機能の追加ウィザード」の「開始する前に」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/3478a19fe0234164b03055238d5fb1ed.png)
1. 「インストールの種類の選択」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「インストールの種類の選択」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/02290a0cb9f5464981a9053a29854e47.png)
1. 「対象サーバの選択」画面が表示されるので対象サーバを選択し「次へ(N)」ボタンをクリックしてください。  
![「対象サーバの選択」画面。対象サーバの一覧がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/f3801966f3d14c7fbd56551b625d5b78.png)
1. 「サーバの役割の選択」画面が表示されるので「Webサーバ(IIS)」にチェックを入れてください。  
![「サーバの役割の選択」画面。「Webサーバ(IIS)」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/b31ff2be4f8d481fa61e0a1bf05eebd7.png)
1. 「Webサーバ(IIS)に必要な機能を追加しますか？」画面が表示されるので「管理ツールを含める(存在する場合)」にチェックを付け、「機能の追加」ボタンをクリックしてください。  
![「Webサーバ(IIS)に必要な機能を追加しますか？」画面。「機能の追加」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/2941c60775d2462baa82e662fdbecec4.png)
1. 「Webサーバ(IIS)」にチェックが入ったことを確認し「次へ(N)」ボタンをクリックしてください。  
![「サーバの役割の選択」画面。「Webサーバ(IIS)」にチェックが入った状態](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/b31ff2be4f8d481fa61e0a1bf05eebd7.png)
1. 「機能の選択」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「機能の選択」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/ccae8556524f435185738c7bf3aa47a1.png)
1. 「Webサーバの役割(IIS)」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「Webサーバの役割(IIS)」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/8b207ad5089c4c09b430fa39589e569d.png)
1. 「役割サービスの選択」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
![「役割サービスの選択」画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/c79b29b6d67a4f34aa27d973455f2f26.png)
1. 「インストールオプションの確認」画面が表示されるので「インストール(I)」ボタンをクリックしてください。  
![「インストールオプションの確認」画面。「インストール(I)」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/8f857e896a13467fabef8f758af12cbd.png)
1.  インストールの完了を待ちます。  
![インストールを実行している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/890fbb6364304633be5125fc5a33a61c.png)
1. インストールの完了後、「閉じる」ボタンをクリックしてください。

## IISの設定変更

1. 「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS)マネージャー」を起動してください。
1. 「アプリケーションプール」の「DefaultAppPool」を選択し、「アプリケーションプール既定値の設定」をクリックしてください。
![IISマネージャーの「アプリケーションプール」画面。「アプリケーションプール既定値の設定」がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/f5ea5c36b6964f21b7159acde5123ede.png)
1. 「プロセスモデル」の「アイドルタイムアウトの操作」を、「Terminate」から「Suspend」に変更し、「OK」をクリックしてください。
![「アプリケーションプール既定値」ダイアログ。「アイドルタイムアウトの操作」を「Suspend」に変更する](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/9ab5568cacd14a568f5b73e1a238c9a7.png)