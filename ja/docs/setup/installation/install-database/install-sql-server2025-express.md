---
title: SQL Server 2025 Expressのインストール及び設定
category: 関連ソフトウェアのインストール
order: '100'
status: ''
parts: ''
urlstring: install-sql-server2025-express
translationKey: install-sql-server2025-express
shortname: ''
created: 2025-12-22
updated: 2026-02-24
---

## 制限事項

SQL Server 2025 Express エディションはデータベースの最大容量が50 GBに制限されています。50 GBを超えて使用する場合には上位Editionへの移行またはMicrosoft Azure SQL Databaseへの移行が必要です。SQL Server 2025 Express エディションの制限については以下ページを参照ください。
[FAQ：SQL Server Expressの制約について教えてください。](../../../FAQ/system-requirements-and-setup/faq-sql-server-express-restriction.md)

## SQL Server 2025 Express エディションのダウンロード

1. 以下のURLにアクセスし、「SQL Server 2025 Express」の「今すぐダウンロード」リンクをクリックしてください。  
https://www.microsoft.com/ja-jp/sql-server/sql-server-downloads
![SQL Server のダウンロードページ。「SQL Server 2025 Express」の「今すぐダウンロード」リンクがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/dc4c193db065486a9cfd566270c3e959.png)
1. ダウンロードしたファイルをダブルクリックしてください。
![ダウンロードしたインストーラのファイルをエクスプローラーで表示したところ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/9b26ea0ee83f4d978d5d4bc590244733.png)
1. 「ユーザー アカウント制御」が表示されたら「はい」ボタンをクリックしてください。  
![「ユーザー アカウント制御」のダイアログ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/2e0aa24b3d394deebfc2b70e909e0d5f.png)
1. 「Download Media」をクリックしてください。  
![SQL Server 2025 Express のインストーラの最初の画面。「Download Media」が選べる](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/0efd9d4828504fe393ef63b24cf212ae.png)
1. 「Japanese」を選択し、「Express Core (718 MB)」にチェックを付け、「Download」ボタンをクリックしてください。
![メディアのダウンロードの画面。「Japanese」と「Express Core (718 MB)」を選んだ状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/552a70e1cd07494db7e73721fbda6fec.png)
1. ダウンロードが完了するまで待ちます。  
![メディアをダウンロード中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/22aa56986690464b8fa2e60883b68433.png)
1. 「Download successful!」と表示されたら「Open folder」ボタンをクリックしてください。  
![「Download successful!」と表示された画面。「Open folder」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/b5fdb47f58f741d385818e2d0a057a66.png)

## SQL Server 2025 Express エディションのインストール

1. 「SQLEXPR_x64_JPN」をダブルクリックしてください。  
![ダウンロード先のフォルダをエクスプローラーで開いたところ。「SQLEXPR_x64_JPN」が置かれている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/b6a313744c6a412faf0f22a15239fe6c.png)
1. 「展開されたファイルのディレクトリの選択」ダイアログが表示されるので「OK」ボタンをクリックしてください。  
![「展開されたファイルのディレクトリの選択」ダイアログ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/93b0eb22c3ac44bf8b490da015ef16d6.png)
1. 展開の準備が完了するまで待ちます。  
![ファイルを展開している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/c13e8fe460d441fbbefd3590a037656c.png)
1. 「SQL Serverの新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加」をクリックしてください。  
![インストールの種類を選ぶ画面。新規スタンドアロン インストールの項目が並んでいる](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/5162de3ac8134bf2bcfb1c9826c561b2.png)
1. 「ライセンス条項と次に同意します」にチェックを付け、「次へ」ボタンをクリックしてください。  
![ライセンス条項の画面。「ライセンス条項と次に同意します」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/3ccd150dd7074da7a1613fe667bc7ab1.png)
1. 「グローバル ルール」の画面はスキップされます。スキップされない場合は、画面の指示に従ってください。
![「グローバル ルール」の画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/2fbe88f742984b0a865250a671c97b36.png)
1. 「Microsoft Update を使用して更新プログラムを確認する (推奨)」をクリックして、「次へ」ボタンをクリックしてください。
![更新プログラムの確認を設定する画面。Microsoft Update を使うかどうかの選択がある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/8f2f1636b7ee42e48b5220f7bbbc555b.png)
1. 「インストール ルール」の画面で「次へ」をクリックしてください。  
![「インストール ルール」の画面。事前チェックの結果が一覧になっている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/a7c394f83b1c47479a70dbfef3dfc26e.png)
1. 環境により、以下の画面が表示される場合があります。表示された場合は、「SQL Server 用 Azure 拡張機能」を無効化して、「次へ」ボタンをクリックしてください。  
![「SQL Server 用 Azure 拡張機能」を無効化する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/38a681a71c8f4c249d43beecf787463d.png)
1. 「データベース エンジン サービス」および「検索のためのフルテキスト抽出とセマンティック抽出」のみにチェックを行い「次へ」ボタンをクリックしてください。  
![インストールする機能を選ぶ画面。「データベース エンジン サービス」などにチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/ff7f90a5f58d4ed49dd9ac88ab8bdf1c.png)
1. 「既定のインスタンス」にチェックし「次へ」ボタンをクリックしてください。  
![インスタンスを選ぶ画面。「既定のインスタンス」にチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/baa0a257f85b4b1e8bc5def00fa247ff.png)
1. 「次へ」ボタンをクリックしてください。  
![インスタンスを選んだ次に表示される設定画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/b8d840e635d7473a9f103b90ecb12660.png)
1. 「混合モード (SQL Server 認証と Windows 認証)」にチェックし、任意のパスワードを設定してください。設定したパスワードは、[プリザンターのインストール](../install-with-installer/getting-started-installer-pleasanter-windows.md)にて使用するため控えてください。その後、「次へ」ボタンをクリックしてください。インストールが始まります。  
![認証モードを設定する画面。「混合モード」を選び、パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/f8e88f04791a4aab814bb3e9d646e214.png)
1. インストールが完了するまで待ちます。  
![インストールを実行している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/092a68d820044b05bc786d75a326f256.png)
1. 正常にインストールされていることを確認し「閉じる」ボタンをクリックしてください。  
![インストールの完了画面。機能ごとの結果が一覧になっている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/5effbab233164e479bdda175f18d8630.png)

## SQL Server 2025 Express エディションの設定

1. 「スタート」ボタンをクリックし、「すべて」-「Microsoft SQL Server 2025」-「SQL Server 2025 構成マネージャー」を起動してください。
1. 左ペインにて「SQL Server ネットワークの構成」-「MSSQLSERVER のプロトコル」とクリックしてください。次に、右ペインにて「TCP/IP」を右クリックし「有効化」をクリックしてください。
![SQL Server 2025 構成マネージャー。「TCP/IP」を右クリックし「有効化」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/470764c0337746e8ac539130ee846353.png)
1. 警告が表示されたら、「OK」ボタンをクリックしてください。
![TCP/IP を有効化したときに表示される警告のダイアログ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/f8f30844935a49d890428f10af88054c.png)
1. 左ペインにて「SQL Serverのサービス」とクリックしてください。次に、右ペインにて「SQL Server (MSSQLSERVER)」を右クリックし「再起動」をクリックしてください。
![SQL Server 2025 構成マネージャー。SQL Server のサービスを右クリックし「再起動」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/31edb3411ae5482b92459f089708413a.png)
1. 再起動が完了したら本手順は完了です。