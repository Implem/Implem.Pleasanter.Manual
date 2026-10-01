---
title: MySQLのインストール（Windows OS）
category: 関連ソフトウェアのインストール
order: '800'
status: ''
parts: ''
urlstring: install-mysql-on-windows
translationKey: install-mysql-on-windows
shortname: ''
created: 2024-09-06
updated: 2026-01-13
---

MySQLをWindows OSにインストールする手順です。 

## 注意事項

1. MySQLはver1.4.9.0以降で使用できます。ver1.4.9.0より前のプリザンターはMySQLに対応していません。

## Microsoft Visual C++ 再頒布可能パッケージのダウンロード

1. 以下のURLにアクセスします。  
https://learn.microsoft.com/ja-jp/cpp/windows/latest-supported-vc-redist?view=msvc-170
2. サポートされている最新の x64 バージョンの固定リンクをクリックし、インストーラをダウンロードします。
![Microsoft Visual C++ 再頒布可能パッケージのダウンロードページ。x64 版の固定リンクがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/e5d7af1a507644aea58563d64df07e40.png)

## Microsoft Visual C++ 再頒布可能パッケージのインストール

1. ダウンロードしたファイルを実行し、最新の Microsoft Visual C++ 再頒布可能パッケージをインストールします。

## MySQLのダウンロード

1. 以下のURLにアクセスします。  
https://dev.mysql.com/downloads/mysql/
2. バージョン「8.4.x LTS」を選択します。
3. 「Windows (x86, 64-bit), MSI Installer」の行の「 Download 」ボタンをクリックします。
![MySQL のダウンロードページ。「Windows (x86, 64-bit), MSI Installer」の行に「Download」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/1bd7ebd2e71f40189fdea840d19cfd72.png)
4. 「No thanks, just start my download.」リンクをクリックしインストーラをダウンロードします。
![ダウンロード開始のページ。「No thanks, just start my download.」リンクがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/c14eee33ded44c77b0ab3dbd75c3794e.png)

## MySQLのインストール

1. ダウンロードしたファイルを実行します。
1. 「Next」ボタンをクリックします。
![MySQL インストーラの最初の画面。「Next」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/66a6346b08f043c79a154348616b0a9a.png)
1. 「I accept the terms in the License Agreement」をチェックし、「Next」ボタンをクリックします。
![ライセンス条項の画面。「I accept the terms in the License Agreement」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/ecab666de63b435cae53ba0a7efd3d24.png)
1. 「 Custom 」ボタンをクリックします。
![セットアップの種類を選ぶ画面。「Custom」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/4ea7311324bd4e8db7487163e4278c26.png)
1. 適宜インストール先（Installation Directory）を変更し、「Next」ボタンをクリックします。（特別な要件がなければそのまま「Next」ボタンをクリックしてください。）
![MySQL のインストール先（Installation Directory）を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/085fbc747fd74a6a9b0c72266ff29514.png)
1. 「Install」ボタンをクリックします。
![インストールの開始を確認する画面。「Install」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/2556fee73e8044138bdde87ddb3c0346.png)
1. 「Run MySQL Configurator」にチェックされていることを確認し、「Finish」ボタンをクリックします。
![インストールの完了画面。「Run MySQL Configurator」のチェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/a131d01f54394e0a80ed1b89e8a30e0d.png)
1. MySQL Configuratorが実行されたことを確認し、「Next >」ボタンをクリックします。
![MySQL Configurator の最初の画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/bad68a975c0f4fdd9fee58e2a7c60ed2.png)
1. 適宜MySQLのデータの保存先（Data Directory）を変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![MySQL のデータの保存先（Data Directory）を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/ff09c9503c9643b38278266e1290b7dd.png)
1. 適宜Config Type、ConnectivityおよびAdvanced Configrationを変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![Config Type、Connectivity、Advanced Configration を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/56b2ebe3f00a40139acd55ec5580760e.png)
1. rootユーザのパスワードを入力し、「Next >」ボタンをクリックします。ここで入力したパスワードは[Rds.json](../../parameters/rds-json.md)の接続文字列の設定で使用しますので、忘れずに記録してください。
![root ユーザのパスワードを入力する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/2ce60573cb9a466d9d658091cf1d05e4.png)
1. 適宜Windows Service NameおよびRun Windows Service as...を変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![Windows Service Name とサービスの実行アカウントを指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/96d3a44b5d4d494b8dba7c447d5a2a98.png)
1. 適宜MySQLのデータファイルのアクセス権を変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![MySQL のデータファイルのアクセス権を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/91805ec08eef43279449e3b36b1864b5.png)
1. 適宜サンプルデータベース作成の要否を変更し、「Next >」ボタンをクリックします。（特別な要件がなければそのまま「Next >」ボタンをクリックしてください。）
![サンプルデータベースを作成するかどうかを選ぶ画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/e1cf17902ce4449e9a6a00bf253c74b8.png)
1. 「Execute」ボタンをクリックします。
![設定内容を適用する画面。「Execute」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/ce392d7feffa47b08b8222b516e59b46.png)
1. インストールが完了するまで待ち、完了後「Next >」ボタンをクリックします。
![設定の適用が完了した画面。「Next >」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/0d05b006a40c4dccbb3e9390d2c684b4.png)
1. 「Finish」ボタンをクリックし、本手順は完了です。
![MySQL Configurator の完了画面。「Finish」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/2bac529841b943e3a295e0ff75e0614b.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.9.0 以降|MySQLへの対応に伴いマニュアルを新規作成|