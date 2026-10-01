---
title: 統合Windows認証によるシングルサインオンを利用する
category: 追加設定：認証
order: '300'
status: ''
parts: ''
urlstring: active-directory-sso
translationKey: active-directory-sso
shortname: 統合Windows認証
created: 2019-04-29
updated: 2025-01-30
---

# 概要

Active Directoryを利用した環境では、統合Windows認証によりプリザンターにシングルサインオンが可能です。

# 前提条件

## サーバの要件

-   Active Directoryにドメイン参加していること。
-   [プリザンターとActive Directoryを連携する](active-directory.md)の設定を行っていること。

## クライアントPCの要件

-   Active Directoryにドメイン参加していること。
-   Active DirectoryドメインユーザでクライアントPCにログインしていること。
-   統合Windows認証をサポートするブラウザを使用していること。
-   コントロールパネルから「インターネットオプション」を開き、下記の設定が行われていること。
    -   「詳細設定」タブ：「統合Windows認証を利用する」にチェックが付いている。
    -   「セキュリティ」タブ：プリザンターサーバのセキュリティゾーンが「イントラネット」または「信頼済みサイト」に登録されている。
    -   「セキュリティ」タブ：セキュリティゾーンのレベルにて「ユーザー認証 - ログオン」の項目が「現在のユーザー名とパスワードで自動的にログオンする」に設定されている。

# 統合Windows認証によるシングルサインオンを設定

1. [Windows認証のインストール](#install-windows-auth) 
2. [Windows認証の有効化](#enable-windows-auth) 
3. [ユーザーの同期やリマインダーなどのバッチ処理を行うための設定](#batch-settings)

## Windows認証のインストール {#install-windows-auth}

1. 「サーバマネージャー」を起動してください。

2. 「管理(M)」メニューを開き「役割と機能の追加」をクリックしてください。  
    ![サーバマネージャーの「管理(M)」メニュー。「役割と機能の追加」が選べる](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/6545a62c94ed4eebb1f32c0bd639b293.png)

3. 「開始する前に」画面が表示されるので「次へ(N)」ボタンをクリックしてください。  
    ![役割と機能の追加ウィザードの「開始する前に」画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/ff7dada7a38443b9b36eeeea398e2487.png)

4. 「インストールの種類の選択」画面が表示されるので「次へ(N)」ボタンをクリックしてください。
    ![役割と機能の追加ウィザードの「インストールの種類の選択」画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/5a183f513934474ba68047f11a86ee44.png)

5. 「サーバの選択」画面が表示されるので対象サーバを選択し「次へ(N)」ボタンをクリックしてください。  
    ![役割と機能の追加ウィザードの「サーバの選択」画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/c276dbd25c204dffa7f889f6a3cfd483.png)

6. 「サーバの役割の選択」画面が表示されるので「Windows 認証」にチェックを入れてください。チェックが入ったことを確認し「次へ(N)」ボタンをクリックしてください。  
    ![「サーバの役割の選択」画面。「Windows 認証」にチェックを入れる](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/6c6a6a6537bb4caaa5c81d1815a9e4d3.png)

7. 「インストールオプションの確認」画面が表示されるので「インストール(I)」ボタンをクリックしてください。  
    ![役割と機能の追加ウィザードの「インストールオプションの確認」画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/49d7892d0e4c4ffaad294e54596cf5af.png)

8. インストールの完了を待ちます。
    ![Windows 認証のインストールが進行中のウィザード画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/e8b64d2accf34fb8b39c99c62d9f8228.png)

9. インストールの完了後、「閉じる」ボタンをクリックしてください。本手順は完了です。
    ![インストールが完了し「閉じる」ボタンが押せる状態のウィザード画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/64766a94b2424425844cbca9c64e28af.png)

## Windows認証の有効化 {#enable-windows-auth}

1. 「インターネット インフォメーション サービス(IIS)マネージャー」を起動します。
    ![インターネット インフォメーション サービス(IIS)マネージャーの画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/e6e94237b2f44542af570c10f8881348.png)

2. 左ペインにて [サイト] -「Default Web Site」をクリックしてください。その後、中央ペインにて[認証](../../../users-guide/hands-on/advanced/advanced-operations-authentication.md)をクリックしてください。
    ![IISマネージャーでDefault Web Siteを選び、中央ペインの「認証」を開くところ](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/2bbd6182aca14f77bf73626814ae846b.png)

3. 「Windows 認証」を"有効"。それ以外を"無効"にします。
    ![IISの認証の一覧。「Windows 認証」だけが有効になっている](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/400b064bab3f44b690faacd6f68c9b44.png)

## ユーザーの同期やリマインダーなどのバッチ処理を行うための設定 {#batch-settings}

統合Windows認証を有効とした環境でLDAPによるユーザーの同期やリマインダーを実行するスクリプトを実行するには、下記の手順でメンテナンス用のアプリケーションを追加する必要があります。

### メンテナンス用アプリケーションプールの作成

匿名認証で実行を行うためにメンテナンス用アプリケーションプールを作成します。

1. 「インターネット インフォメーション サービス(IIS)マネージャー」を起動します。

2. 左ペインにて「アプリケーションプール」を選択し、右側の「操作」にて「アプリケーションプールの追加...」をクリックしてください。

3. 下記を入力し「OK」をクリックします。

    |項目名|設定値|
    |:---|:---|
    |名前|任意の名前を設定（例：MainteAppPool）|
    |.Net CLRバージョン|マネージドコードなし|
    |マネージドパイプラインモード|統合|
    |アプリケーションプールを直ちに開始する|オン|

    ![IISの「アプリケーションプールの追加」ダイアログの入力例](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/a5074864dea04daba2fadf33513ca7be.png)

4. [サイト] を右クリックし「Webサイトの追加」をクリックします。
5. 下記を入力し「OK」をクリックします。

    |項目名|設定値|
    |:---|:---|
    |サイト名|任意の名前を設定（例：Mainte Site）|
    |アプリケーションプール|前の手順で作成したものを選択（例：MainteAppPool）|
    |コンテンツディレクトリ - 物理パス|C:\web\pleasanter\Implem.Pleasanter|
    |バインド - 種類|http|
    |バインド - IPアドレス|未使用のIPアドレスすべて|
    |バインド - ポート|8080（任意のポート）|
    |バインド - ホスト名|（ブランク）|
    |Web サイトを直ちに開始する|オン|

    ![IISの「Webサイトの追加」ダイアログの入力例（Mainte Site、ポート8080）](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/1688a644915b41838e6fa4fd2aec7ac8.png)

6. Mainte Siteをクリックし、認証をダブルクリックし下記のように設定してください。

    |項目名|設定値|
    |:---|:---|
    |匿名認証|有効|
    |上記以外|すべて無効|

    ![Mainte Siteの認証の一覧。匿名認証だけが有効になっている](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/099023a452b742b686423dfc66426658.png)

7. 画面右側の「*.8080(http)参照」をクリックしてプリザンターのログイン画面が起動することを確認します。

### LDAPによるユーザー同期／リマインダー／API実行の設定  

下記手順に従って、設定を行います。

  - 「プリザンターのリマインダー機能を有効化する（外部スクリプト）」 
  - 「プリザンターにActive Directoryのユーザ情報を同期する（外部スクリプト）」  

その際、上記2.の手順で指定した「ポート」を処理実行時のURLとするように設定してください。

(例) ポートを"8080"とした場合

-   ユーザー同期のURL: http://{ServerName}:8080/users/syncbyldap
-   リマインダーのURL: http://{ServerName}:8080/reminderschedules/remind?NoLog=1
-   API実行のURL: http://{ServerName}:8080/api/items/{レコードID}/get

### AbsoluteUriの設定  

上記URLでリマインダーの実行やAPI経由の更新で通知などが行われる場合には、メールに記載されるURLが上記となってしまう問題を避けるため、Service.json の AbsoluteUri に通常のプリザンターのURLを設定してください。  
 [パラメータ設定：Service.json](../../parameters/service-json.md)

|項目名|設定値|
|:---|:---|
|AbsoluteUri|http://{ServerName}|