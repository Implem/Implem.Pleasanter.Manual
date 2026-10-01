---
title: PostgreSQL 17のインストール（Windows OS）
category: 関連ソフトウェアのインストール
order: '700'
status: ''
parts: ''
urlstring: install-postgresql17-on-windows
translationKey: install-postgresql17-on-windows
shortname: ''
created: 2025-12-23
updated: 2026-01-13
---

PostgreSQL 17をWindows OSにインストールする手順です。 

## 制限事項

1. PostgreSQL 18をWindows OSにインストールする手順は[こちら](install-postgresql-on-windows.md)を参照してください。
1. Azure ADの組織アカウントなど全角文字のアカウントでログインした状態ではPostgreSQLインストーラでエラーが発生する可能性があります。その場合は半角文字のアカウントでログインし直してインストーラを実行してください。

## PostgreSQL 17のダウンロード

1. 以下URLにアクセスし、Windows x86-64の中からインストールしたいバージョンのモジュールをダウンロードしてください。  
https://www.enterprisedb.com/downloads/postgres-postgresql-downloads
![PostgreSQL のダウンロードページ。Windows x86-64 のバージョンごとのリンクが並んでいる](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/1e1016c702d3475890dd6a638828f17f.png)

## PostgreSQL 17のインストール

1. ダウンロードしたファイルを実行します。
「Next >」ボタンをクリックします。
![PostgreSQL 17 インストーラの最初の画面。「Next >」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/538cfb6dd0fe44309591775532145a36.png)
1. 適宜インストール先（Installation Directory）を変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![インストール先（Installation Directory）を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/2da1c88002ad422598c1454681505ae1.png)
1. 「PostgreSQL Server」と「pgAdmin 4」にチェックされていることを確認し、「Next >」ボタンをクリックします。（その他のコンポーネントは適宜選択してください。特別な要件がなければすべてにチェックし、「Next >」ボタンをクリックしてください。）
![インストールするコンポーネントを選ぶ画面。「PostgreSQL Server」と「pgAdmin 4」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/60d5cc50dd4e41d5b80277f4a1820bcf.png)
1. 適宜データファイルの保存先（Data Directory）を変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![データファイルの保存先（Data Directory）を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/af25e2e37ec14d138d698d725fbaeb27.png)
1. postgresユーザのパスワードを入力し、「Next >」ボタンをクリックします。ここで入力したパスワードは[Rds.json](../../parameters/rds-json.md)の接続文字列の設定で使用しますので、忘れずに記録してください。
![postgres ユーザのパスワードを入力する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/65f4fd2c7fc64f49a332fd5104e9948d.png)
1. 適宜ポート番号を変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![ポート番号を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/135595f5dc29425dbb7c397eea0a1285.png)
1. 適宜ロケールを変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![ロケールを選ぶ画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/63d4aed4bc4e4c858c33a5b35c156ad4.png)
1. 「Next >」ボタンをクリックします。
![設定内容を確認する画面。「Next >」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/198cab15d2da4e578c0e19483c4e1919.png)
1. 「Next >」ボタンをクリックします。
![インストールの開始を確認する画面。「Next >」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/1f379dd62e3740669fc206dc0cffafa7.png)
1. インストールが完了するまで待ちます。
![インストールを実行している途中の進捗画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/944b89119b7746778ad6adc87c9c685c.png)
1. 「Finish」ボタンをクリックし、本手順は完了です。
![PostgreSQL 17 インストーラの完了画面。「Finish」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/f6d13c7089cf498988f7bb71d1a1206e.png)