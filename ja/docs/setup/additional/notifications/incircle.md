---
title: InCircleに通知できるように設定する
category: 追加設定：通知
order: '800'
status: ''
parts: ''
urlstring: incircle
translationKey: incircle
shortname: ''
created: 2021-10-01
updated: 2024-06-07
---

## InCircle側の設定

※InCircleのユーザ登録を行っていることが必要です。
　ログイン手順の詳細についてはInCircleの下記トップページより右上の「既存のお客様」をクリックして
　ユーザーサポートのページへ遷移後、操作マニュアルを参照してください。
　https://www.bluetec.co.jp/incircle/

### API機能の有効化

1.管理コンソールにて［API］→［API 設定］画面の API 機能を［有効］にして、［保存］ボタンを押下します。
![InCircle管理コンソールの［API 設定］画面。API機能を［有効］にする](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/6d8bc2e1be88445f9afce97022eb4da8.png)

### APIユーザの作成

1.管理コンソールの［ユーザとグループ］→［新規ユーザ登録］画面にて API ユーザを作成します。
![InCircle管理コンソールの［新規ユーザ登録］画面。APIユーザを作成する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/825a36f3fb504398b1f2028b648122ae.png)

### APIトークンの取得

1.［ユーザとグループ］→［ユーザ編集］画面にて、上記で作成した API ユーザの［変更］ボタンを押下します。
![InCircleの［ユーザ編集］画面。APIユーザの［変更］ボタンを押す](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/f1739d1a1cc24d1e9c3039eea245c3d9.png)

2.［アクセストークン］タブを選択します。［トークン ID 作成］ボタンを押下します。
![InCircleの［アクセストークン］タブ。［トークン ID 作成］ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/88e8dd18f3044f2d8fc2cd3c694ec1d6.png)

3.作成された［トークン ID］を任意の箇所にコピーしておきます。

### 新しいトークの作成

1.標準ユーザで InCircle にログインし、API ユーザを選択して新しいトークを作成します。
![InCircleでAPIユーザを選び、新しいトークを作成するところ](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/9ceb5788dc5c4f8fa3232ddefa766ba9.png)

### トーク番号の取得

1.POST送信が可能なツールを準備してください。（Postmanなど）

2.Bodyを以下のとおり入力してください。

　token_id：上記で作成した［トークン ID］を設定します。
　action：1（固定）

3.以下のURLを指定してPOST送信してください。

　https://{ホスト}.incircle.jp/{コード}/api/v1/ticketL.do

4.レスポンスからメッセージを送信したいトークの［ticketno］を確認します。この番号がトーク番号です。

## プリザンター側の設定

1.通知を設定するテーブルを選択し、[テーブルの管理](../../../managers-guide/manage-table/index.md)-[通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)タブを開いてください。「新規作成」ボタンをクリックしてください。

![テーブルの管理の「通知」タブ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/39ee5f48ad504b2ca817d752b990344c.png)

2.通知種別で「InCircle」を選択してください。アドレスおよびトークンに以下を入力し、「追加」ボタンをクリックしてください。

　アドレス → https://{ホスト}.incircle.jp/{コード}/api/v1/messageC.do
　トークン → {トーク番号}:{トークンID}　（トーク番号とトークンIDをコロン（:）で区切る）

![通知の設定画面。通知種別「InCircle」でアドレスとトークンを入力する](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/24c3fafd540340779c0969e14dbbb891.png)

3.「変更」ボタンをクリックしてください。設定後、指定した通知タイミングで以下のように通知が行われます。
![InCircleのトークに届いたプリザンターの通知の例](https://pleasanter.org/files/images/ja/setup/additional/notifications/assets/1db50e9adf974fe88e18c4d0cd98ab55.png)

## 関連情報

-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [応用編：通知、リマインダー](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)
