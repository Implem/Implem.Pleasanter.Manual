---
title: パスキー認証を利用する
category: 追加設定：認証
order: '0'
status: ''
parts: ''
urlstring: passkey
translationKey: passkey
shortname: パスキー認証
created: 2026-01-13
updated: 2026-04-15
---

## 制限事項

1. パスキー認証と二段階認証の両方が有効な環境では以下の挙動となります。

    -   パスキー認証でログインした場合、二段階認証画面は表示されません。
    -   ID、パスワードでログインした場合、二段階認証画面が表示されます。
1. パスキー認証はHTTPSコンテキストでのみ利用可能です。
1. ブラウザにパスワードマネージャ拡張機能がインストールされている場合、Windows セキュリティより優先的に処理が実行される場合があります。Windows セキュリティによる認証を利用する場合は、拡張機能の処理をキャンセルしてください。
1. 認証処理の途中、一定時間が経過するとタイムアウトし、ユーザにその旨が通知されます。ユーザにより認証の中断操作が行われた場合も同様です。必要に応じて手順を再度実行してください。
1. パスキー認証は、Windows 11以降、macOS 13.0（Ventura）以降、iOS 16.0以降、iPad OS 以降、Android 9.0以降の各OSでサポートされています。
1. Webブラウザは常に最新版にアップデートしてご利用ください。
1. QRコードの読み取りは、各OS標準のカメラアプリを用いてください。
1. AndroidにおいてカメラアプリでQRコードを読み取れない場合は、Googleレンズをご利用ください。

## 概要

パスキー認証を使用するには、以下の設定が必要です。  

## サーバ側の設定

[Authentication.json](../../parameters/authentication-json.md)のPasskeyParameters以下の各パラメータを設定してください。 

```json
{
    ...
　   "PasskeyParameters": {
　       "Enabled": true,
　       "ServerName": "Pleasanter",
　       "ServerDomain": "servername1",
　       "Origins": [ "https://servername1", "https://servername1:443" ]
         "UserVerificationRequirement": "Preferred"
　   },
    ...
}
```

#### PasskeyParameters以下のパラメータ一覧

|パラメータ名|設定例|説明|
|-|-|-|
|Enabled|true| パスキー認証の有効化・無効化を切り替えます。デフォルト値はfalseです。|
|ServerName|"Pleasanter"|（nullや空文字以外の）任意の文字列を指定してください。|
|ServerDomain|"localhost"|以下のOriginsに設定するURLのドメイン部分を設定してください。|
|Origins| ["https://servername1", "https://severname1:443"]|ユーザがブラウザでアクセスするURLを指定してください。登録されていないURLからのログイン試行は拒否されます。ポート番号が異なる場合、別のURLとして扱われます。|
|UserVerificationRequirement|Preferred|サーバがデバイスに対して、User Verification（デバイスの使用者がユーザ本人であることをローカルで確認する操作―PIN入力、指紋認証、顔認証などのこと、以下UV）を求めるか否かを以下の3つの値で設定します。<br><br>**Required**<br>デバイスにUVを**必ず要求**します。UVに対応していないデバイスでは操作が失敗します。<br><br>**Preferred**<br>デバイスにUVを**可能であれば要求**します。デバイスがUVに対応していない場合は、認証なしで続行します。<br><br>**Discouraged**<br>デバイスにUVを**要求しない**ことを推奨します。ただし、デバイスがUVするポリシーであれば無視されます。|

UserVerificationRequirement はデバイスに対するポリシー宣言ですが、デバイス自身がUVを常に要求するポリシーを持つ場合（Windows Hello、iPhoneなど）、設定値に関わらずUVが実行されます。このため、そのようなデバイスのみを対象とする環境では、設定値による動作差は生じません。

## クライアント側の設定

クライアント側ではパスキーの作成と保存が必要です。手順はパスキーの保存先に応じて異なります。

<details markdown="1">
<summary style="font-weight:bold; color:darkblue">📱 スマートフォンへ保存する</summary>

パスキーを作成し、作成したパスキーをスマートフォンへ保存する手順を説明します。事前にスマートフォンの設定アプリでBluetoothをオンにしてください。

1. パスキーを作成するアカウントでプリザンターへログインしてください。このログインには、パスキー認証以外の認証方式を用います。
1. ナビゲーションメニューの[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)をクリックしてください。
1. [プロファイル編集](../../../users-guide/common/profile.md)をクリックしてください。
1. コマンドボタンエリアの「パスキー」ボタンをクリックしてください。  
   ![プロファイル編集画面のコマンドボタンエリア。「パスキー」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/ac2bb4606d4840c5bb9986de09c683f2.png)
1. 「パスキー」ダイアログが表示されます。「新規作成」ボタンをクリックしてください。  
   ![「パスキー」ダイアログ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/67d48ae7a67046638562b3fc072b9442.png)
1. パスキーの保存先をスマートフォンへ変更します。「変更」をクリックしてください。
   ![パスキーの保存先を確認する画面。「変更」が選べる](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/ff4639317a9c405985a20e32770c8e1e.png)
1. 「iPhone、iPad、または Android デバイス」をクリックしてください。
   ![パスキーの保存先の選択肢。「iPhone、iPad、または Android デバイス」がある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/72827ceb46b94bd99420a25ccbf9b55d.png)
1. 表示される QR コードをスマートフォンのカメラアプリで読み取り、「パスキーを保存」をタップしてください。  
   ![パソコンの画面に表示されたパスキー保存用のQRコード](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/d7a2548eac654c08809d0a0cc4e661b8.png)　![QRコードを読み取ったスマートフォンの「パスキーを保存」の画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/894dcfc2b1a24f3cb04c16753db8823d.png)
1. スマートフォンにパスキーを追加します。「パスキーを追加」ボタンをタップしてください。このときスマートフォンのユーザ認証を求められます。  
 ![スマートフォンの「パスキーを追加」ボタンが表示された画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/a2d4b827c3914ee49e130053616808e2.png)
1. パスキーがスマートフォンに保存されると、「パスキー」ダイアログに作成されたキーが表示されます。「閉じる」ボタンをクリックしてください。
   ![「パスキー」ダイアログ。作成されたパスキーが表示されている](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/99f0fd680d9b4c888dfbc9b7c3e8f411.png)
</details>

<details markdown="1">
<summary style="font-weight:bold; color:darkblue">💻 Windowsへ保存する</summary>

パスキーを作成し、作成したパスキーをWindowsへ保存する手順を説明します。

1. パスキーを作成するアカウントでプリザンターへログインしてください。このログインには、パスキー認証以外の認証方式を用います。
1. ナビゲーションメニューの[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)をクリックしてください。
1. [プロファイル編集](../../../users-guide/common/profile.md)をクリックしてください。
1. コマンドボタンエリアの「パスキー」ボタンをクリックしてください。  
   ![プロファイル編集画面のコマンドボタンエリア。「パスキー」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/ac2bb4606d4840c5bb9986de09c683f2.png)
1. 「パスキー」ダイアログが表示されます。「新規作成」ボタンをクリックしてください。  
   ![「パスキー」ダイアログ。「新規作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/67d48ae7a67046638562b3fc072b9442.png)
1. 「続行」ボタンをクリックしてください。  
   ![Windowsへパスキーを保存する画面。「続行」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/8128c3ce84c245a4b82a23df83eb4ce5.png)
1. Windows Helloによる本人確認を済ませます。以下は暗証番号 (PIN) による認証画面です。  
   ![Windows Helloの暗証番号(PIN)による本人確認の画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/c0937f635ec34552b82f68c5af0f8a48.png)
1. 本人確認が済むと、「パスキー」ダイアログに作成されたキーが表示されます。「閉じる」ボタンをクリックしてください。  
   ![「パスキー」ダイアログ。Windowsに保存したパスキーが表示されている](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/7f6fdc15a64f416ea40407a619417e80.png)
</details>

<details markdown="1">
<summary style="font-weight:bold; color:darkblue;">🔑 その他の保存先へ保存する</summary>

上記以外にも、以下をパスキーの保存先として利用できます。詳細は各製品のドキュメントを確認してください。

1. セキュリティ キー
1. ブラウザ拡張機能として提供されるサードパーティ製パスワードマネージャ
1. ブラウザに組み込まれたパスワードマネージャ

なお、上記のうち「3. ブラウザに組み込まれたパスワードマネージャ」を選択する場合は、Windows セキュリティによるパスキー保存をキャンセルしてください。

![Windows セキュリティによるパスキー保存の画面。ここをキャンセルする](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/ad85ce0281674147bd736bdbe10ee91f.png)

フォールバックして、選択できるようになります。

![キャンセル後に表示される、パスキーの保存先を選び直せる画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/f4fa7a685f4344ebb2cf9a5748a8ac95.png)
</details>

## ログイン手順

「🔑その他の保存先への保存」を選択した場合のログイン手順については、画面の指示に従ってください。

<details markdown="1">
<summary style="font-weight:bold; color:darkblue">📱 スマートフォンに保存したパスキーでログインする</summary>

1. パスキーを作成したアカウントでログイン画面を開き、「パスキーでログイン」ボタンをクリックしてください。
   ![プリザンターのログイン画面。「パスキーでログイン」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/698387624bee44daa181126bea4e26ad.png)
1. 保存したパスキータイプを選択します。「iPhone、iPad、または Android デバイス」をクリックしてください。  
  ![パスキーの種類の選択。「iPhone、iPad、または Android デバイス」がある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/e3cc045721c24f62a3bc1cd0a81acfa3.png)
1. 表示される QR コードをスマートフォンのカメラアプリで読み取り、「パスキーでログイン」をタップしてください。  
   ![パソコンの画面に表示されたログイン用のQRコード](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/fb02c0eb31834b45a3a737a850398c49.png)　![QRコードを読み取ったスマートフォンの「パスキーでログイン」の画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/19c05f1fe17341688fe951bb1e922826.png)
1. スマートフォンの画面下部に、確認メッセージが表示されます。「パスキーを使用」ボタンをタップしてください。このときスマートフォンのユーザ認証を求められます。  
   ![スマートフォンの画面下部に出る確認メッセージ。「パスキーを使用」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/529c26076f5f42d3a685141d134494dc.png)

以上で、プリザンターへログインできます。
</details>

<details markdown="1">
<summary style="font-weight:bold; color:darkblue">💻 Windowsに保存したパスキーでログインする</summary>

1. パスキーを作成したアカウントでログイン画面を開き、「パスキーでログイン」ボタンをクリックしてください。
   ![プリザンターのログイン画面。「パスキーでログイン」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/698387624bee44daa181126bea4e26ad.png)
1. Windows Helloによる本人確認を済ませます。以下は暗証番号 (PIN) による認証画面です。  
   ![ログイン時のWindows Helloの暗証番号(PIN)による本人確認の画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/4aa4ebe22da44b16b3ab857b79719a5f.png)

以上で、プリザンターへログインできます。
</details>

## パスキーの編集

作成したパスキーのタイトル（名前）を変更したり、不要になったパスキーをプリザンターから削除したりできます。

<details markdown="1">
<summary style="font-weight:bold; color:darkblue">パスキーのタイトルを変更する</summary>

1. プリザンターへログインしてください。
1. ナビゲーションメニューの[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)をクリックしてください。
1. [プロファイル編集](../../../users-guide/common/profile.md)をクリックしてください。
1. コマンドボタンエリアの「パスキー」ボタンをクリックしてください。  
1. 「パスキー」ダイアログで、変更したいパスキーをクリックしてください。  
   ![「パスキー」ダイアログ。一覧から変更したいパスキーを選ぶ](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/03a28958b4604a30a907ca8666bd5e62.png)
1. 「パスキーの編集」ダイアログが表示されます。[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)を編集し、「変更」ボタンをクリックしてください。  
   ![「パスキーの編集」ダイアログ。タイトルを編集して「変更」ボタンを押す](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/69baaa99458045778d0c9d218e217dd4.png)
1. 「パスキーの編集」ダイアログが閉じ、タイトルの変更を確認できます。「閉じる」ボタンをクリックしてください。  
   ![タイトルの変更が反映された「パスキー」ダイアログ](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/f46adeb129284aee92d4e29e165348be.png)
</details>

<details markdown="1">
<summary style="font-weight:bold; color:darkblue">パスキーを削除する</summary>

1. プリザンターへログインしてください。
1. ナビゲーションメニューの[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)をクリックしてください。
1. [プロファイル編集](../../../users-guide/common/profile.md)をクリックしてください。
1. コマンドボタンエリアの「パスキー」ボタンをクリックしてください。  
1. 削除したいパスキーの左側のチェックボックスをクリックして有効化し、[削除](../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)ボタンをクリックしてください。  
   ![「パスキー」ダイアログ。削除するパスキーのチェックボックスと「削除」ボタン](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/f57ca4baf201459e926a77089d87d154.png)
1. 確認ダイアログが表示されるので、内容を確認し、「OK」ボタンをクリックしてください。
   ![パスキー削除の確認ダイアログ。「OK」ボタンがある](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/77020ad3c48f4d809cd038b7ee4616e2.png)
1. 「操作」ダイアログが閉じ、パスキーが削除されていることを確認できます。  
   ![パスキーが削除された後の「パスキー」ダイアログ](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/7eb00ddcf9bf4336bae56bb855cd603a.png)
1. 必要に応じて、各OSやWebブラウザなどから保存したパスキーを削除してください。保存場所は各製品のマニュアルを確認してください。
</details>

## 対応バージョン

|対応バージョン|内容|
|-|-|
|1.5.1.0 以降|機能追加|
|1.5.3.0 以降|Authentication.jsonへパラメータUserVerificationRequirementを追加|

## 関連情報

-   [パラメータ設定：Authentication.json](../../parameters/authentication-json.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [共通機能：プロファイル編集](../../../users-guide/common/profile.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../managers-guide/tenant-administration/tenant-logo.md)
-   [テーブル機能：レコードの削除](../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)