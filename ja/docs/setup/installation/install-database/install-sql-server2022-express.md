---
title: SQL Server 2022 Expressのインストール及び設定
category: 関連ソフトウェアのインストール
order: '200'
status: ''
parts: ''
urlstring: install-sql-server2022-express
translationKey: install-sql-server2022-express
shortname: ''
created: 2023-06-08
updated: 2026-01-13
---

## 制限事項

SQL Server 2022 Express with Advanced Servicesはデータベースの最大容量が10GBに制限されています。10GBを超えて使用する場合には上位Editionへの移行またはMicrosoft Azure SQL Databaseへの移行が必要です。SQL Server 2022 Express  の制限については以下ページを参照ください。
[FAQ：SQL Server Expressの制約について教えてください。](../../../FAQ/system-requirements-and-setup/faq-sql-server-express-restriction.md)

## SQL Server 2022 Express with Advanced Servicesのダウンロード

1. 以下のURLにアクセスしExpress エディションの「 ダウンロード 」ボタンをクリックしてください。  
https://www.microsoft.com/ja-jp/download//details.aspx?id=104781  
1. ファイルのダウンロードが完了したら「実行(R)」ボタンをクリックしてください。  
1. 「次のプログラムにこのコンピュータへの変更を許可しますか？」と表示されるので「はい(Y)」ボタンをクリックしてください。  
1. 「メディアのダウンロード(D)」をクリックしてください。  
![SQL Server 2022 Express のインストーラの最初の画面。「メディアのダウンロード(D)」が選べる](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/2a11eceb6df547538a0c864aa5101ef9.png)
1. 「Express Advanced」にチェックを付け、「ダウンロード(D)」ボタンをクリックしてください。
![メディアのダウンロードの画面。「Express Advanced」にチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/4cddf46c79c74d3a83127183064616bc.png)
1. ダウンロードが完了するまで待ちます。  
![メディアをダウンロード中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/b9a56be7518344eeaf81d0e812538729.png)
1. 「ダウンロードに成功しました。」と表示されたら「フォルダーを開く」ボタンをクリックしてください。  
![「ダウンロードに成功しました。」と表示された画面。「フォルダーを開く」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/c2068d7be9864dbb8fb08b4278c5b2cb.png)

## SQL Server 2022 Express with Advanced Servicesのインストール

1. 「SQLEXPRADV_x64_JPN」をダブルクリックしてください。  
![ダウンロード先のフォルダをエクスプローラーで開いたところ。「SQLEXPRADV_x64_JPN」が置かれている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/4595522b2e67478eb56ec6c94a03040f.png)
1. 「展開されたファイルのディレクトリの選択」ダイアログが表示されるので「OK」ボタンをクリックしてください。  
![「展開されたファイルのディレクトリの選択」ダイアログ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/ba99ff889ac24622b4c7fc40125a0a69.png)
1. 展開の準備が完了するまで待ちます。  
![ファイルを展開している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/8326f01cc5634fbb8a582e9ab00968b2.png)
1. 「SQL Serverの新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加」をクリックしてください。  
![インストールの種類を選ぶ画面。新規スタンドアロン インストールの項目が並んでいる](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/1aed965899814760a73601cf4da0d4ec.png)
1. 「ライセンス条項と次に同意します」にチェックし「次へ(N)>」ボタンをクリックしてください。  
![ライセンス条項の画面。「ライセンス条項と次に同意します」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/7bb99d61f8154ea798e46dfbccfbabaa.png)
1. 「グローバル ルール」の画面はスキップされます。スキップされない場合は、画面の指示に従ってください。
![「グローバル ルール」の画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/6c0e38827f9b427d9ff8ba328e35ece1.png)
1. 「Microsoft Update を使用して更新プログラムを確認する (推奨)」をクリックして、「次へ」ボタンをクリックしてください。
![更新プログラムの確認を設定する画面。Microsoft Update を使うかどうかの選択がある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/0da5d3ec878144a2ab4195b28e667421.png)
1. 「インストール ルール」の画面で「次へ(N)」をクリックしてください。  
![「インストール ルール」の画面。事前チェックの結果が一覧になっている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/6f97154240684a878fb1f2ecff8e3bf1.png)
1. 「データベース エンジン サービス」および「検索のためのフルテキスト抽出とセマンティック抽出」のみにチェックを行い「次へ(N)>」ボタンをクリックしてください。  
![インストールする機能を選ぶ画面。「データベース エンジン サービス」などにチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/8f670eb645a644a0965b4d11049fdbb5.png)
1. 「既定のインスタンス(D)」にチェックし「次へ(N)>」ボタンをクリックしてください。  
![インスタンスを選ぶ画面。「既定のインスタンス(D)」にチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/e7018d689a3e4c3b957e8256c5685653.png)
1. 「次へ(N)>」ボタンをクリックしてください。  
![インスタンスを選んだ次に表示される設定画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/8d72967e06be43d5b7570c20e2a15103.png)
1. 「混合モード(SQL Server 認証と Windows 認証)(M)」にチェックし、任意のパスワードを設定してください。設定したパスワードは、[プリザンターのインストール](../install-with-installer/getting-started-installer-pleasanter-windows.md)にて使用するため控えてください。その後、「次へ(N)>」ボタンをクリックしてください。インストールが始まります。  
![認証モードを設定する画面。「混合モード」を選び、パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/3f883de1176b4f98836b525962f73a5a.png)
1. インストールが完了するまで待ちます。  
![インストールを実行している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/b112d1b959d14e8fa92180966129427a.png)
1. 正常にインストールされていることを確認し「閉じる」ボタンをクリックしてください。  
![インストールの完了画面。機能ごとの結果が一覧になっている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/a55cbe7bed224c78b5cdedf52bfd90ae.png)

## SQL Server 2022 Express with Advanced Servicesの設定

1. 「スタート」ボタンをクリックし、「すべて」-「Microsoft SQL Server 2022」-「SQL Server 2022 構成マネージャー」を起動してください。
1. 左ペインにて「SQL Server ネットワークの構成」-「MSSQLSERVERのプロトコル」とクリックしてください。次に、右ペインにて「TCP/IP」を右クリックし「有効化にする(E)」をクリックしてください。
![SQL Server 2022 構成マネージャー。「TCP/IP」を右クリックし「有効化にする(E)」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/47217ec5e9b54936bc29e462f0d8e65c.png)
1. 左ペインにて「SQL Serverのサービス」とクリックしてください。次に、右ペインにて「SQL Server(MSSQLSERVER)」を右クリックし「再起動(T)」をクリックしてください。
![SQL Server 2022 構成マネージャー。SQL Server のサービスを右クリックし「再起動(T)」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/49af33a351b648b287a07c9b2e6f0676.png)
1. 再起動が完了したら本手順は完了です。