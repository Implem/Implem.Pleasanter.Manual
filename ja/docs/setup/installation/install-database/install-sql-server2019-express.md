---
title: SQL Server 2019 Expressのインストール及び設定
category: 関連ソフトウェアのインストール
order: '300'
status: ''
parts: ''
urlstring: install-sql-server2019-express
translationKey: install-sql-server2019-express
shortname: ''
created: 2021-03-26
updated: 2026-01-13
---

## 制限事項

SQL Server 2019 Express with Advanced Servicesはデータベースの最大容量が10GBに制限されています。10GBを超えて使用する場合には上位Editionへの移行またはMicrosoft Azure SQL Databaseへの移行が必要です。SQL Server 2019 Express  の制限については以下ページを参照ください。
[FAQ：SQL Server Expressの制約について教えてください。](../../../FAQ/system-requirements-and-setup/faq-sql-server-express-restriction.md)  

## SQL Server 2019 Express with Advanced Servicesのダウンロード

1. 以下のURLにアクセスしダウンロードボタンをクリックしてください。  
https://www.microsoft.com/ja-jp/download/details.aspx?id=101064

1. ファイルのダウンロードが完了したら「実行(R)」ボタンをクリックしてください。 

1. 「次のプログラムにこのコンピュータへの変更を許可しますか？」と表示されるので「はい(Y)」ボタンをクリックしてください。  

1. 「メディアのダウンロード(D)」をクリックしてください。  
![SQL Server 2019 Express のインストーラの最初の画面。「メディアのダウンロード(D)」が選べる](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/19ee2beedc434808b5508647774b4fc1.png)

1. 「Express Advanced」にチェックを付け、「ダウンロード(D)」ボタンをクリックしてください。
![メディアのダウンロードの画面。「Express Advanced」にチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/435aa43f28bb4bf787eab94bc584ad56.png)

1. ダウンロードが完了するまで待ちます。  
![メディアをダウンロード中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/edfd88bf88da449e8fb561d27c56622c.png)

1. 「ダウンロードに成功しました。」と表示されたら「フォルダーを開く」ボタンをクリックしてください。  
![「ダウンロードに成功しました。」と表示された画面。「フォルダーを開く」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/db05fe421f9c401d8f594e1f4e0c0da4.png)

## SQL Server 2019 Express with Advanced Servicesのインストール

1. 「SQLEXPRADV_x64_JPN」をダブルクリックしてください。  
![ダウンロード先のフォルダをエクスプローラーで開いたところ。「SQLEXPRADV_x64_JPN」が置かれている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/4595522b2e67478eb56ec6c94a03040f.png)

1. 「展開されたファイルのディレクトリの選択」ダイアログが表示されるので「OK」ボタンをクリックしてください。  
![「展開されたファイルのディレクトリの選択」ダイアログ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/ba99ff889ac24622b4c7fc40125a0a69.png)

1. 展開の準備が完了するまで待ちます。  
![ファイルを展開している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/ce0e699c7a2e40449492b2089481b99e.png)

1. 「SQL Serverの新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加」をクリックしてください。  
![インストールの種類を選ぶ画面。新規スタンドアロン インストールの項目が並んでいる](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/cd314d87573f4e749c83807d411fcb5e.png)

1. 「ライセンス条項に同意します。(A)」にチェックし「次へ(N)>」ボタンをクリックしてください。  
![ライセンス条項の画面。「ライセンス条項に同意します。(A)」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/4ac17bbe90a549a9b3d3600943fd5e17.png)

1. 「Microsoft Update を使用して更新プログラムを確認する(推奨)(M)」をチェックし「次へ(N)>」ボタンをクリックしてください。  
![更新プログラムの確認を設定する画面。Microsoft Update を使うかどうかのチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/28c85deaf9bd4a19b4c114b9cb9f084a.png)

1. 「インストール ルール」の画面で「次へ(N)」をクリックしてください。  
![「インストール ルール」の画面。事前チェックの結果が一覧になっている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/e8cef077c54b4b7da878b3aae71bb6ad.png)

1. 「データベース エンジン サービス」および「検索のためのフルテキスト抽出とセマンティック抽出」のみにチェックを行い「次へ(N)>」ボタンをクリックしてください。  
![インストールする機能を選ぶ画面。「データベース エンジン サービス」などにチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/4910e947389848499ecd4ede7e71eaf8.png)

1. 「既定のインスタンス(D)」にチェックし「次へ(N)>」ボタンをクリックしてください。  
![インスタンスを選ぶ画面。「既定のインスタンス(D)」にチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/9b7f6c4650da4452befcd01a651b6236.png)

1. 「次へ(N)>」ボタンをクリックしてください。  
![インスタンスを選んだ次に表示される設定画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/44346476a3e949a3a8c4dbb05b7d6958.png)

1. 「混合モード(SQL Server 認証と Windows 認証)(M)」にチェックし、任意のパスワードを設定してください。設定したパスワードは、[プリザンターのインストール](../../../FAQ/system-requirements-and-setup/faq-install-linux-apache.md)にて使用するため控えてください。その後、「次へ(N)>」ボタンをクリックしてください。  
![認証モードを設定する画面。「混合モード」を選び、パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/538232843dc24324ae906dd836ae2f63.png)

1. インストールが完了するまで待ちます。  
![インストールを実行している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/581f5765a659435bb1b0b7cd0f7576cf.png)

### ※エラー：1638 が発生した場合、Microsoft Visual C++2017をアンインストールしてから、再度SQL Serverのインストールを行ってください。

1. 正常にインストールされていることを確認し「閉じる」ボタンをクリックしてください。  
![インストールの完了画面。機能ごとの結果が一覧になっている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/0fde2692c5b14e2db8a2d862ac7814b5.png)

## SQL Server 2019 Express with Advanced Servicesの設定

1. スタートボタンをクリック、「Microsoft SQL Server 2019」-「SQL Server 2019 構成マネージャー」を起動してください。

1. 左ペインにて「SQL Server ネットワークの構成」-「MSSQLSERVERのプロトコル」を選択してください。その後、右ペインにて「TCP/IP」を右クリックし「有効化(E)」をクリックしてください。
![SQL Server 2019 構成マネージャー。「TCP/IP」を右クリックし「有効化(E)」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/51be7415af4c49b38c870933e357e717.png)

1. 左ペインにて「SQL Serverのサービス」を選択してください。そして、右ペインにて「SQL Server(MSSQLSERVER)」を選択し「再起動(T)」をクリックしてください。
![SQL Server 2019 構成マネージャー。SQL Server のサービスを選び「再起動(T)」を選ぶところ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/afb07e817431439b9fbd60353d591516.png)

1. 再起動が完了したら本手順は完了です。