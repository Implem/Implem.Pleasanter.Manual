---
title: PostgreSQL 18のインストール（Windows OS）
category: 関連ソフトウェアのインストール
order: '600'
status: ''
parts: ''
urlstring: install-postgresql-on-windows
translationKey: install-postgresql-on-windows
shortname: ''
created: 2023-10-19
updated: 2026-01-13
---

PostgreSQL 18をWindows OSにインストールする手順です。 

## 制限事項

Azure ADの組織アカウントなど全角文字のアカウントでログインした状態ではPostgreSQLインストーラでエラーが発生する可能性があります。その場合は半角文字のアカウントでログインし直してインストーラを実行してください。

## PostgreSQL 18のダウンロード

1. 以下URLにアクセスし、Windows x86-64の中からインストールしたいバージョンのモジュールをダウンロードしてください。  
https://www.enterprisedb.com/downloads/postgres-postgresql-downloads
![PostgreSQL のダウンロードページ。Windows x86-64 のバージョンごとのリンクが並んでいる](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/73e5f18c0da9421e8b1fde9919be1a3a.png)

## PostgreSQL 18のインストール

1. ダウンロードしたファイルを実行します。ユーザーアクセス制御が表示された場合は「はい」をクリックしてください。
「Next >」ボタンをクリックしてください。
![PostgreSQL 18 インストーラの最初の画面。「Next >」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/00289ea4193943ec80c6306502f82c36.png)
1. 適宜インストール先（Installation Directory）を変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![インストール先（Installation Directory）を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/9f4cf8a45ba74443b7a24da69a06d1a8.png)
1. 「PostgreSQL Server」と「pgAdmin 4」にチェックされていることを確認し、「Next >」ボタンをクリックします。（その他のコンポーネントは適宜選択してください。特別な要件がなければすべてにチェックし、「Next >」ボタンをクリックしてください。）
![インストールするコンポーネントを選ぶ画面。「PostgreSQL Server」と「pgAdmin 4」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/0762fd9591a14f91b146b15ca86a51d1.png)
1. 適宜データファイルの保存先（Data Directory）を変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![データファイルの保存先（Data Directory）を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/b8b2d6f5332443bab06a0db498e29b0f.png)
1. postgresユーザのパスワードを入力し、「Next >」ボタンをクリックします。ここで入力したパスワードは[Rds.json](../../parameters/rds-json.md)の接続文字列の設定で使用しますので、忘れずに記録してください。
![postgres ユーザのパスワードを入力する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/54a5b8316f6f4a80af90baa166c64eaf.png)
1. 適宜ポート番号を変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![ポート番号を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/eff95cd34179412ba808a914033e1a0d.png)
1. 適宜ロケールを変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![ロケールを選ぶ画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/2115dd0752954661acffdf1e180881bd.png)
1. 「Next >」ボタンをクリックします。
![設定内容を確認する画面。「Next >」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/0669491ebb0544b7942ad9ed84adf0c7.png)
1. 「Next >」ボタンをクリックします。
![インストールの開始を確認する画面。「Next >」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/d342686e12fb4a9a88624bf0ce90aa11.png)
1. インストールが完了するまで待ちます。
![インストールを実行している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/10625c99a2a94c92ac1f83ab0d63277a.png)
1. 「Finish」ボタンをクリックし、本手順は完了です。
![PostgreSQL 18 インストーラの完了画面。「Finish」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/b9b5d53161304bc3baa825ad68b97844.png)