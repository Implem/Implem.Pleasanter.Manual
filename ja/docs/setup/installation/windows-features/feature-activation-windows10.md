---
title: Windowsの機能の有効化（Windows 11）
category: Windowsの機能の有効化
order: '500'
status: ''
parts: ''
urlstring: feature-activation-windows10
translationKey: feature-activation-windows10
shortname: ''
created: 2019-04-29
updated: 2026-01-13
---

## 概要

本手順では、プリザンターの動作に必要となるIISおよびASP.NETの有効化を行います。

## Windowsの機能の有効化

1. スタートメニューから「コントロールパネル」を起動してください。  

1. 「プログラム」をクリックしてください。  
![コントロールパネルの画面。「プログラム」の項目がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/df8b39444e804ed792262f7bfc37b582.png)

1. 「Windowsの機能の有効化または無効化」をクリックしてください。  
![コントロールパネルの「プログラム」画面。「Windowsの機能の有効化または無効化」がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/7c93172d270b4ff2a80bbeda34db59fb.png)

1. 「インターネットインフォメーションサービス」以下の「IIS管理コンソール」、「静的なコンテンツ」、「ASP.NET 4.7」(環境により「ASP.NET 4.6」、「ASP.NET 4.8」の場合もあります)にチェックを付け(それらをチェックした際に自動的に追加される項目はそのままで構いません)、下図のようになっている事を確認し「OK」ボタンをクリックしてください。
![「Windowsの機能」ダイアログ。「IIS管理コンソール」「静的なコンテンツ」「ASP.NET 4.7」にチェックを付けた状態](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/b7c780a712b346889b271d2bb844800b.png)

1. 「Windows Update からファイルをダウンロードする」をクリックしてください。  
(選択した機能が既にインストールされている場合、この画面は表示されません。次の手順へ進んでください。）
![「Windows Update からファイルをダウンロードする」を選ぶ画面](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/027288de5028405382b15da9421dbc39.png)

1. 「閉じる」ボタンをクリックしてください。
![機能の変更が完了した画面。「閉じる」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/e0ff7be68a784176b1598af5381e705f.png)

## IISの設定変更

1. スタートメニューから「インターネットサービス（IIS)マネージャー」を起動してください。

1. 「アプリケーションプール」の「DefaultAppPool」を選択し、「アプリケーションプール既定値の設定」をクリックしてください。
![IISマネージャーの「アプリケーションプール」画面。「アプリケーションプール既定値の設定」がある](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/f5ea5c36b6964f21b7159acde5123ede.png)
1. 「プロセスモデル」の「アイドルタイムアウトの操作」を、「Terminate」から「Suspend」に変更し、「OK」をクリックしてください。
![「アプリケーションプール既定値」ダイアログ。「アイドルタイムアウトの操作」を「Suspend」に変更する](https://pleasanter.org/files/images/ja/setup/installation/windows-features/assets/9ab5568cacd14a568f5b73e1a238c9a7.png)
