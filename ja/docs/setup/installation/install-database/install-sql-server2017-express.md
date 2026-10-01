---
title: SQL Server 2017 Expressのインストール及び設定
category: 関連ソフトウェアのインストール
order: '400'
status: ''
parts: ''
urlstring: install-sql-server2017-express
translationKey: install-sql-server2017-express
shortname: ''
created: 2019-04-28
updated: 2026-01-13
---

## 制限事項

SQL Server 2017 Express with Advanced Servicesはデータベースの最大容量が10GBに制限されています。10GBを超えて使用する場合には上位Editionへの移行またはMicrosoft Azureへの移行が必要です。SQL Server 2017 Express  の制限については以下ページを参照ください。
[FAQ：SQL Server Expressの制約について教えてください。](../../../FAQ/system-requirements-and-setup/faq-sql-server-express-restriction.md)  

## SQL Server 2017 Express with Advanced Servicesのダウンロード

1. 以下のURLにアクセスしダウンロードボタンをクリックしてください。  
https://www.microsoft.com/ja-jp/download/details.aspx?id=55994

1. ファイルのダウンロードが完了したら「実行(R)」ボタンをクリックしてください。 

1. 「次のプログラムにこのコンピュータへの変更を許可しますか？」と表示されるので「はい(Y)」ボタンをクリックしてください。  

1. 「メディアのダウンロード(D)」をクリックしてください。  
![SQL Server 2017 Express のインストーラの最初の画面。「メディアのダウンロード(D)」が選べる](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/815d78f03fcf4cf293e87cdf5254ec34.png)

1. 「Express Advanced」にチェックを付け、「ダウンロード(D)」ボタンをクリックしてください。
![メディアのダウンロードの画面。「Express Advanced」にチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/b6dcbc25ec97495483ea3205aaae7a66.png)

1. ダウンロードが完了するまで待ちます。  
![メディアをダウンロード中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/45d4ccf057bd4818b7eaa1f13a7129b8.png)

1. 「ダウンロードに成功しました。」と表示されたら「フォルダーを開く」ボタンをクリックしてください。  
![「ダウンロードに成功しました。」と表示された画面。「フォルダーを開く」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/6464bf14c430451882706c6599d927ee.png)

## SQL Server 2017 Express with Advanced Servicesのインストール

1. 「SQLEXPRADV_x64_JPN」をダブルクリックしてください。  
![ダウンロード先のフォルダをエクスプローラーで開いたところ。「SQLEXPRADV_x64_JPN」が置かれている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/963f83c2bb944058b4aec2036fa8e373.png)

1. 「展開されたファイルのディレクトリの選択」ダイアログが表示されるので「OK」ボタンをクリックしてください。  
![「展開されたファイルのディレクトリの選択」ダイアログ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/2fc6e310689243e8a9f72775794386fe.png)

1. 展開の準備が完了するまで待ちます。  
![ファイルを展開している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/9667943f9da244399dff217a11810515.png)

1. 「SQL Serverの新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加」をクリックしてください。  
![インストールの種類を選ぶ画面。新規スタンドアロン インストールの項目が並んでいる](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/60c219f219014eb5b3ec5ec2d4612d24.png)

1. 「ライセンス条項に同意します。(A)」にチェックし「次へ(N)>」ボタンをクリックしてください。  
![ライセンス条項の画面。「ライセンス条項に同意します。(A)」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/6f2928b04bee482db71c5a4bfeebf4dd.png)

1. 「Microsoft Update を使用して更新プログラムを確認する(推奨)(M)」をチェックし「次へ(N)>」ボタンをクリックしてください。  
![更新プログラムの確認を設定する画面。Microsoft Update を使うかどうかのチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/3cb122779dc34a0a8df27b0976aef42d.png)

1. 「インストール ルール」の画面で「次へ(N)」をクリックしてください。  
![「インストール ルール」の画面。事前チェックの結果が一覧になっている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/354ec977bc2a4f5d966b8335c89b49c4.png)

1. 「データベース エンジン サービス」および「検索のためのフルテキスト抽出とセマンティック抽出」のみにチェックを行い「次へ(N)>」ボタンをクリックしてください。  
![インストールする機能を選ぶ画面。「データベース エンジン サービス」などにチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/7c3bc2ffd1d64d0c98e5d007de818d69.png)

1. 「既定のインスタンス(D)」にチェックし「次へ(N)>」ボタンをクリックしてください。  
![インスタンスを選ぶ画面。「既定のインスタンス(D)」にチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/c890627b62174f4b9f67dbb443914305.png)

1. 「次へ(N)>」ボタンをクリックしてください。  
![インスタンスを選んだ次に表示される設定画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/b56276b6b6d84ff286caa0aa96aa8d53.png)

1. 「混合モード(SQL Server 認証と Windows 認証)(M)」にチェックし、任意のパスワードを設定してください。設定したパスワードは、[プリザンターのインストール](../../../FAQ/system-requirements-and-setup/faq-install-linux-apache.md)にて使用するため控えてください。その後、「次へ(N)>」ボタンをクリックしてください。  
![認証モードを設定する画面。「混合モード」を選び、パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/26aaf028132c495cb19fa747524929ad.png)

1. インストールが完了するまで待ちます。  
![インストールを実行している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/1aa1ff560b5c40b4b17d0b7a68cfb331.png)

## ※エラー：1638 が発生した場合、Microsoft Visual C++2017をアンインストールしてから、再度SQL Serverのインストールを行ってください。

1. 正常にインストールされていることを確認し「閉じる」ボタンをクリックしてください。  
![インストールの完了画面。機能ごとの結果が一覧になっている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/62881e96a88842eaafb1121b01a136aa.png)

## SQL Server 2017 Express with Advanced Servicesの設定

1. スタートボタンをクリック、「Microsoft SQL Server 2017」-「SQL Server 2017 構成マネージャー」を起動してください。

1. 左ペインにて「SQL Server ネットワークの構成」-「MSSQLSERVERのプロトコル」を選択してください。その後、右ペインにて「TCP/IP」を右クリックし「有効化(E)」をクリックしてください。
![SQL Server 2017 構成マネージャー。「TCP/IP」を右クリックし「有効化(E)」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/ccf5007ba2cc490685f1501813bdfc39.png)

1. 左ペインにて「SQL Serverのサービス」を選択してください。そして、右ペインにて「SQL Server(MSSQLSERVER)」を選択し「再起動(T)」をクリックしてください。
![SQL Server 2017 構成マネージャー。SQL Server のサービスを選び「再起動(T)」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/8f83f2e769694a5ab23f030744452642.png)

1. 再起動が完了したら本手順は完了です。