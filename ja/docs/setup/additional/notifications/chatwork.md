---
title: Chatworkに通知できるように設定する
category: 追加設定：通知
order: '400'
status: ''
parts: ''
urlstring: chatwork
translationKey: chatwork
shortname: ''
created: 2019-04-30
updated: 2025-01-30
---

## 前提条件

chatworkのユーザ登録を行ってください。  
http://www.chatwork.com/ja/

## room IDおよびAPIトークンの取得

chatworkにログインしてください。  
http://www.chatwork.com/ja/

### room IDの取得

1. URLの#!ridより右の番号を控えてください。この番号がroom IDです。
![ChatworkのURL。#!ridより右の番号がroom ID](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/196330e52542476caad41304e70f9737.png)

### APIトークンの取得

1. 画面右上のユーザ名をクリックし、環境設定を開いてください。
![Chatwork画面右上のユーザ名のメニュー。環境設定を開くところ](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/5f3bb88c04a3462ca746d5cfe58dd683.png)

1. 画面左のAPI Tokenクリックし、API Token設定を開いてください。
![Chatworkの環境設定画面。左側に「API Token」がある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/0ef4075d769b4f2694839ac5359e5455.png)

1. チャットワークのパスワードを入力し、「表示」ボタンをクリックしてください。
![API Token設定画面。パスワードを入力して「表示」ボタンを押す](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/ca6b6ccc747e46aca690ecfc27527d4d.png)

1. 表示されたAPIトークンを控えてください。
![ChatworkのAPIトークンが表示された画面](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/f8e70456165a423c91e53c6c3425dde5.png)

## プリザンターの設定

1.通知を設定するテーブルを選択し、[テーブルの管理](../../../managers-guide/manage-table/index.md)-[通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブを開いてください。「新規作成」ボタンをクリックしてください。
![テーブルの管理の「通知」タブ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/53e3eecaab3d44028c0a087fc6ed413d.png)

2.通知種別で「chatwork」を選択してください。アドレスおよびトークンに以下を入力し、「追加」ボタンをクリックしてください。
* アドレス　→　https://api.chatwork.com/v2/rooms/{room ID}/messages  
{room ID}部分は、控えていたroom IDに置き換えてください。
* トークン　→　控えていたAPIトークン

![通知の設定画面。通知種別「chatwork」でアドレスとトークンを入力する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/70e6c13c516c4fadb7ca0e436ba396e2.png)

3.「更新」ボタンをクリックしてください。以上で本手順は完了です。
![テーブルの管理画面。「更新」ボタンで設定を保存する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/af3687167daf49bf89b44816b943a9f7.png)