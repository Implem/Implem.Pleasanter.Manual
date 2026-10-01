---
title: SQLでレコードを抽出する
category: 開発支援ツール
order: '9000'
status: ''
parts: ''
urlstring: development-tools-execute-sql
translationKey: development-tools-execute-sql
shortname: Pleasanter Extensions,Development Tools,SQLでレコードを抽出
created: 2025-01-27
updated: 2025-02-14
---

## 概要

任意のSQLを実行し、データベースからレコードを抽出します。抽出したレコードはSQLResult画面で表示します。

- SQLを記述したSQLファイルを選択し、実行します。
![SQLファイルを選択して実行するところ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/development-tools/assets/e7cfd6f56248448592427f024ae287d6.png)

- 抽出したレコード一覧がSQLResult画面で表示されます。
![抽出したレコード一覧を表示するSQLResult画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/development-tools/assets/abf8347a5cfa4e8d976a76288d14254d.png)

## 操作手順

<div class="steps" markdown>

1. [Settings.json](development-tools-setup.md)をエディタで開きます。
1. Environments に実行するSQLファイルを配置した環境の Environment を追加します。Name / Title / Dbms / ConnectionString を設定します。
1. UserSqls に実行するUserSQLファイルの Path を設定します。Description には、当該SQLの説明を記述します。
1. Implem.PleasanterManagementStudio.exe を起動します。
1. 環境の一覧から対象の環境をクリックして選択します。
1. [UserSQL]タブをクリックして表示される任意のUserSQLファイルのPathを選択します。
1. 画面上部のメニューから [Run]-[UserSQL]-[Execute SQL] をクリックします。UserSQLファイルの Path のダブルクリックでも実行できます。
1. ダイアログの確認事項をチェックし「はい(Y)」をクリックします。
1. レコードの抽出結果が表示されます。

</div>

## 関連情報

-   [Development Tools：セットアップ、起動方法](development-tools-setup.md)
