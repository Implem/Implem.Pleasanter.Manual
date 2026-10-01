---
title: SQLServerからWindowsイベントビューアーへ出力されるログの量を抑えたい
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-sql-server-auto-close
translationKey: faq-sql-server-auto-close
shortname: SQLServer
created: 2022-01-27
updated: 2024-12-19
---

## 回答

SQL Serverの「自動終了オプション」を無効にしてください。

---

## 概要

SQLServerの設定「自動終了オプション」が有効となっている場合、データベースは自動で終了し、アクセスが発生する都度起動するようになります。このタイミングでWindowsのイベントビューアへログが出力されるため、状況によっては大量のログが出力されることがあります。以下にログ出力を抑えるため、自動終了オプションを無効にする設定を示します。

## 操作手順

1. SQL Server Management Studioを起動してプリザンターのデータベースサーバに接続してください。
1. 「オブジェクト エクスプローラー」のツリーから「データベース」、「Implem.Pleasanter」の右クリックメニューから、プロパティをクリックしてください。
1. プロパティメニューから、「オプション」を選択し、表示されたパラメータ一覧から「自動終了」を選択してください。
1. 自動終了の設定値を「False」に変更し、「OK」をクリックしてください。
![データベースのプロパティの「オプション」。自動終了を False にする](https://pleasanter.org/files/images/ja/FAQ/operations-and-maintenance/assets/0d1a79f30b3d48d0959a689613bb53e6.png)
